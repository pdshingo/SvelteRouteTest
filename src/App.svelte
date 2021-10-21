<script>
  import { Router, Route, Link } from "svelte-navigator";
  import Login from "./Login.svelte";
  import PrivateRoute from "./PrivateRoute.svelte";
  import { user } from "./stores";
  import { Nav, NavItem, NavLink } from 'sveltestrap';

  function handleLogout() {
    $user = null;
  }
</script>

<Router>
  <header>
    <h1>History</h1>

    <nav>
      <Link to="/">Home</Link>
      <Link to="about">About</Link>
      <Link to="profile">Profile</Link>
    </nav>
    <Nav>
      <NavItem>
        <NavLink href="/">Home</NavLink>
      </NavItem>
      <NavItem>
        <NavLink href="about">About</NavLink>
      </NavItem>
      <NavItem>
        <NavLink href="profile">Profile</NavLink>
      </NavItem>
      <NavItem>
        <NavLink disabled href="#">Disabled Link</NavLink>
      </NavItem>
    </Nav>
  </header>

  <main>
    <Route path="login">
      <Login />
    </Route>

    <Route path="/">
      <h3>Home</h3>
      <p>Home sweet home...</p>
    </Route>

    <Route path="about">
      <h3>About</h3>
      <p>That's what it's all about!</p>
    </Route>

    <PrivateRoute path="profile" let:location>
      <h3>Welcome {$user.username}</h3>
      <button on:click={handleLogout}>Logout</button>
    </PrivateRoute>
  </main>
</Router>
