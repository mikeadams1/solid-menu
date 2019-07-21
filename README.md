# solid-menu
solid menu boilerplate
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Join Solid</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.7.1/css/bulma.min.css">
  <script defer src="https://use.fontawesome.com/releases/v5.3.1/js/all.js"></script>
</head>

<body>

  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="https://bulma.io">
      Solid
    </a>

      <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
    </div>

    <div id="navbarBasicExample" class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item">
        Home
      </a>

        <a class="navbar-item">
        Documentation
      </a>

        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link">
          More
        </a>

          <div class="navbar-dropdown">
            <a class="navbar-item">
            About
          </a>
            <a class="navbar-item">
            Contact
          </a>
            <hr class="navbar-divider">
            <a class="navbar-item">
            Report an issue
          </a>
          </div>
        </div>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">

          <div class="buttons">
            <a id="register" href="https://solid.inrupt.com/get-a-solid-pod" target="_blank" class="button is-primary">
                     <strong>Sign up</strong>
                     </a>
            <a id="login" class="button is-light">
                     Login
                     </a>
            <a id="logout" class="button is-light" style="display:none">
                     Logout
                     </a>
          </div>

        </div>
      </div>
    </div>
  </nav>

  <section class="section">
    <div class="container">
      <h1 class="title">
        App goes here...
      </h1>
      <section id="app" style="display:none">
        <hr>
        <a id="user" target="_blank" href="#"></a>
        <hr>
      </section>
    </div>
  </section>
  <script src="https://melvincarvalho.github.io/helloworld/scripts/jquery.js"></script>
  <script src="https://melvincarvalho.github.io/helloworld/scripts/solid-auth-client.bundle.js"></script>
  <script src="https://melvincarvalho.github.io/helloworld/scripts/rdflib.min.js"></script>
  <script>
    function renderLogin(webId) {
      console.log('logged in as', webId)
      let logout = document.getElementById("logout");
      let login = document.getElementById("login");
      let register = document.getElementById("register");
      let app = document.getElementById("app");
      logout.style.display = "";
      register.style.display = "none";
      login.style.display = "";
      app.style.display = "";
      user.style.display = "";
      user.textContent = webId;
      user.setAttribute("href", webId);
    }
    function renderLogout() {
      let logout = document.getElementById("logout");
      let login = document.getElementById("login");
      let register = document.getElementById("register");
      let app = document.getElementById("app");
      logout.style.display = "none";
      app.style.display = "none";
      login.style.display = "";
      register.style.display = "";
    }
    function handleLogin() {
      // login event
      solid.auth.trackSession(session => {
        if (session && session.webId) {
          renderLogin(session.webId);
        } else {
          renderLogout();
        }
      });
    }
    // Log the user in and out on click
    function addListeners() {
      let login = document.getElementById("login");
      let logout = document.getElementById("logout");
      // login and logout buttons
      const popupUri = "https://melvincarvalho.github.io/helloworld/popup.html";
      login.addEventListener("click", () => solid.auth.popupLogin({
        popupUri
      }));
      logout.addEventListener("click", () => solid.auth.logout());
      handleLogin();
    }
    function hamburgerHelper() {
      document.querySelector(".navbar-burger").addEventListener("click", toggleNav);
      function toggleNav() {
        var nav = document.querySelector(".navbar-menu");
        if (nav.className == "navbar-menu") {
          nav.className = "navbar-menu is-active";
        } else {
          nav.className = "navbar-menu";
        }
      }
    }
    addListeners();
    hamburgerHelper();
  </script>

</body>

</html>
