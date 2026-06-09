---
parent: "[[SidebarMenu]]"
section: composition
component: SidebarMenu
package: "@8x8/oxygen-sidebar-menu"
category: navigation
pipeline_stage: draft
tags:
  - oxygen
  - component/SidebarMenu
  - role/composition
  - stage/draft
  - category/navigation
---

## Two implementation patterns

The package supports two usage styles:

1. **Config-driven (`<Sidebar>`)** — pass a flat `items` array; collapse state is managed internally.
2. **Declarative** — compose `SidebarContainer`, `MenuList`, `MenuItem`, `SubMenuItem`, and `CollapseItem` manually for full control over state.

---

## Pattern 1: Config-driven with `<Sidebar>`

### Item config data

```tsx
import {
  HomeIcon, GearIcon, ChannelsIcon, UsersIcon,
  ArchiveIcon, FeedbackIcon, FaqIcon,
} from '@8x8/oxygen-icons';

const items: SidebarItemProps[] = [
  {
    label: 'Home',
    icon: <HomeIcon />,
    link: '/home',
  },
  {
    label: 'Setup',
    icon: <GearIcon />,
    link: '/setup',
  },
  {
    label: 'Channels with longer text',
    icon: <ChannelsIcon />,
    link: '/channels',
    subItems: [
      { label: 'Channel one', link: '/channels/channel_one' },
      { label: 'Channel two', link: '/channels/channel_two' },
      { label: 'Channel three', link: '/channels/channel_three' },
    ],
  },
  {
    label: 'Agents & Supervisors',
    icon: <UsersIcon />,
    link: '/agents_and_supervisors',
  },
  // footer items
  {
    label: 'Audit log events',
    icon: <ArchiveIcon />,
    link: '/audit-log-events',
    isFooter: true,
  },
  {
    label: 'Send feedback',
    icon: <FeedbackIcon />,
    isFooter: true,
  },
  {
    label: 'Help',
    icon: <FaqIcon />,
    link: '/help',
    isFooter: true,
  },
];
```

### State management hook for config-driven usage

```tsx
const useSidebarState = ({
  action,
  initialRoute,
  badgeOnMenuLinks,
  badgeChildren,
  badgeAriaLabel,
}: {
  action: any;
  initialRoute: string;
  badgeOnMenuLinks?: string;
  badgeChildren?: string;
  badgeAriaLabel?: string;
}) => {
  const [currentRoute, setCurrentRoute] = useState('');
  const badgeOnMenuLinksArray = (badgeOnMenuLinks || '')
    .split(',')
    .map(link => link.trim());

  useEffect(() => {
    if (initialRoute) setCurrentRoute(initialRoute);
  }, [initialRoute]);

  useEffect(() => {
    action(currentRoute);
  }, [action, currentRoute]);

  const createOnTrigger = (item: ItemProps) => () => {
    if (item.link) setCurrentRoute(item.link);
    action('onTrigger')(item);
  };

  const sidebarItems: SidebarItemProps[] = items.map(item => {
    const { label, icon, isFooter, subItems, link } = item;
    const hasBadge = link && badgeOnMenuLinksArray.includes(link);

    return {
      label,
      link,
      icon,
      isFooter,
      hasBadge,
      badgeChildren,
      badgeAriaLabel,
      subItems: subItems?.map(subItem => ({
        ...subItem,
        onTrigger: createOnTrigger(subItem),
        isActive: subItem.link === currentRoute,
        hasBadge: subItem.link && badgeOnMenuLinksArray.includes(subItem.link),
        badgeChildren,
        badgeAriaLabel,
      })),
      onTrigger: createOnTrigger(item),
      isActive: item.link === currentRoute,
    };
  });

  return { sidebarItems, setCurrentRoute };
};
```

### Helper to derive all routes from items

```tsx
const getRoutes = (items: ItemProps[]) => {
  return items
    .flatMap(item => (item.subItems ? [item, ...item.subItems] : item))
    .map(item => item.link)
    .filter(Boolean);
};
```

---

### Render

Wire the resulting `sidebarItems` array into `<Sidebar>` along with collapse labels:

```tsx
import { Sidebar } from '@8x8/oxygen-sidebar-menu';

// sidebarItems derived from useSidebarState above
<Sidebar
  items={sidebarItems}
  collapseLabel="Collapse navigation"
  expandLabel="Expand navigation"
/>
```

---

## Pattern 2: Declarative composition

Full manual control — useful when the consuming app manages collapse state externally (e.g. persisting it to a store).

```tsx
import {
  SidebarContainer,
  MenuList,
  MenuItem,
  SubMenuItem,
  CollapseItem,
} from '@8x8/oxygen-sidebar-menu';
import { useSidebar } from './useSidebar'; // app-level hook

const MySidebar: React.FC<{ collapseLabel: string; expandLabel: string }> = ({
  collapseLabel,
  expandLabel,
}) => {
  const [currentItem, setCurrentItem] = useState('');
  const sidebar = useSidebar();

  const createOnTrigger = (itemName: string) => () => setCurrentItem(itemName);
  const isActive = (itemName: string) => currentItem === itemName;

  return (
    <SidebarContainer collapsed={sidebar.isSidebarCollapsed} position="left">
      <MenuList>
        {/* Simple item */}
        <MenuItem
          label="Users"
          icon={<UsersIcon />}
          onTrigger={createOnTrigger('Users')}
          isActive={isActive('Users')}
        />

        {/* Item with badge */}
        <MenuItem
          label="Badge with count"
          icon={<UsersIcon />}
          onTrigger={createOnTrigger('BadgeChildren')}
          isActive={isActive('BadgeChildren')}
          hasBadge
          badgeChildren="99+"
        />

        {/* Item with sub-menu */}
        <MenuItem label="Platform" icon={<GearIcon />}>
          <SubMenuItem
            label="Company"
            onTrigger={createOnTrigger('Company')}
            isActive={isActive('Company')}
          />
          <SubMenuItem
            label="Contacts With Extra Words To Span 2 Rows"
            onTrigger={createOnTrigger('Contacts')}
            isActive={isActive('Contacts')}
          />
          <SubMenuItem
            label="Calls"
            onTrigger={createOnTrigger('Calls')}
            isActive={isActive('Calls')}
          />
        </MenuItem>

        {/* Item with badge and badged sub-items */}
        <MenuItem label="Badge menus" icon={<GearIcon />} hasBadge>
          <SubMenuItem
            label="with a longer menu label"
            onTrigger={createOnTrigger('BadgeMenuLong')}
            isActive={isActive('BadgeMenuLong')}
            hasBadge
            badgeChildren="99+"
          />
          <SubMenuItem
            label="badge submenu"
            onTrigger={createOnTrigger('BadgeMenuShort')}
            isActive={isActive('BadgeMenuShort')}
            hasBadge
          />
          <SubMenuItem
            label="no badge"
            onTrigger={createOnTrigger('BadgeNo')}
            isActive={isActive('BadgeNo')}
          />
        </MenuItem>
      </MenuList>

      {/* Collapse toggle */}
      <CollapseItem
        label={sidebar.isSidebarCollapsed ? expandLabel : collapseLabel}
      />

      {/* Footer items */}
      <MenuList footer>
        <MenuItem
          label="Long Item Name That Spans On Multiple Rows"
          icon={<ArchiveIcon />}
          onTrigger={() => {}}
        />
      </MenuList>
    </SidebarContainer>
  );
};
```

---

## Badge variants

| Variant | Props |
|---|---|
| No badge | (omit `hasBadge`) |
| Dot badge | `hasBadge` |
| Count badge | `hasBadge badgeChildren="99+"` |
| Accessible badge | `hasBadge badgeAriaLabel="99 unread notifications"` |

---

## Pattern 3: Router integration

Pass a router link component via `linkComponent` and the URL prop name via `linkProp`. Both `<Sidebar>` and `<MenuItem>` support these props — items render as real router links without requiring custom `onTrigger` handlers for navigation.

### With `<Sidebar>` (config-driven)

```tsx
import { Link } from 'react-router-dom';
import { Sidebar } from '@8x8/oxygen-sidebar-menu';

<Sidebar
  items={sidebarItems}
  linkComponent={Link}
  linkProp="to"
  collapseLabel="Collapse navigation"
  expandLabel="Expand navigation"
/>
```

### With `<MenuItem>` (declarative)

```tsx
import { Link } from 'react-router-dom';
import { SidebarContainer, MenuList, MenuItem } from '@8x8/oxygen-sidebar-menu';

<SidebarContainer collapsed={isSidebarCollapsed} position="left">
  <MenuList>
    <MenuItem
      label="Home"
      icon={<HomeIcon />}
      link="/home"
      linkComponent={Link}
      linkProp="to"
      isActive={location.pathname === '/home'}
    />
  </MenuList>
</SidebarContainer>
```

_Source: Oxygen MCP · Extracted 2026-05-07_
