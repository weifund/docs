WeiFund implements a number of defensive practices on the WeiFund front-end code. Here are some of the defensive practices implemented.

- Anti-Script and Cross-Site Script Injection Prevention (XSS)
- Rigid Data Checking of Campaign Contract Data Information
- No direct handling of Etheruem wallets (no wallet creation)
- Re-entracy limiting with Claim Contract distancing
- Separation of concerns for Campaign Templates that don't mix campaign logic with dispersal logic
