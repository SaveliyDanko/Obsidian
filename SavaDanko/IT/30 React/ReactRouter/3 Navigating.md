
[Navigating](https://reactrouter.com/start/declarative/navigating)

---
###### **NavLink**
This component is for navigation links that need to render an active state.
```jsx
import { NavLink } from "react-router";

export function MyAppNav() {
  return (
    <nav>
      <NavLink to="/" end>
        Home
      </NavLink>
      <NavLink to="/trending" end>
        Trending Concerts
      </NavLink>
      <NavLink to="/concerts">All Concerts</NavLink>
      <NavLink to="/account">Account</NavLink>
    </nav>
  );
}
```
Whenever a `NavLink` is active, it will automatically have an `.active` class name for easy styling with CSS:
```css
a.active {
  color: red;
}
```

###### **Link**
Use `<Link>` when the link doesn't need active styling:
```jsx
import { Link } from "react-router";

export function LoggedOutMessage() {
  return (
    <p>
      You've been logged out.{" "}
      <Link to="/login">Login again</Link>
    </p>
  );
}
```