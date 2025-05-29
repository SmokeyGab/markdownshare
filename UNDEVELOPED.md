## Frontend TBD/Mocked Features (Comprehensive Page Review)

Based on a review of frontend page components (`frontend/casinoxmr-app/src`), the following features are currently using mock data, are marked as TBD/TODO, or have unimplemented functionalities:

*   **Content - Game Guides (`GameGuideDetailPage.tsx`, `GameGuidesListPage.tsx`):**
    *   Data fetching for game guides uses mock data (`mockGameGuidesFull`, `mockGameGuides`).
    *   Explicit `TODO` comments to replace mock data with actual data fetching strategies.
    *   `GameGuidesListPage.tsx` has a `TODO` to add filtering/search functionality.

*   **Content - Blog (`BlogListPage.tsx`, `BlogPostPage.tsx`):**
    *   Data fetching for blog posts and individual post content uses mock data (`mockBlogPosts`, `mockBlogPostsFull`).
    *   Explicit `TODO` comments to replace mock data with actual data fetching (e.g., API call or markdown parsing).
    *   `BlogListPage.tsx` has a `TODO` to add pagination.

*   **Affiliate Program (`AffiliateProgramPage.tsx`):**
    *   Affiliate registration (`handleAffiliateRegister`) and login (`handleAffiliateLogin`) functionalities are placeholders (show alerts). Actual implementation of forms/modals or navigation to a portal is pending.

*   **Promotions (`PromotionsPage.tsx`):**
    *   Fetches promotions using mock data (`mockPromotions`).
    *   `useEffect` and `handleClaimPromotion` simulate API calls, with comments indicating they need to be replaced with real API calls.

*   **Info - Contact Us (`ContactUsPage.tsx`):**
    *   Contact form submission (`handleSubmit`) is simulated (logs to console, shows alert). Actual backend integration is pending.
    *   Placeholder email address `support@casinoxmr.example.com`.
    *   Live Chat feature is commented out and marked "Coming Soon".
    *   FAQ data is static; might be intended to be dynamic in a full implementation.

*   **Home Page (`HomePage.tsx`):**
    *   Uses placeholder data for `featuredGames` and `currentPromotion` (comment indicates this should come from API/state).
    *   Uses placeholder image paths that need to be replaced with actual assets.

*   **Games - General (affecting all game pages like `DiceGamePage.tsx`, `MinesGamePage.tsx`, etc., primarily through `useGame.ts`):**
    *   The `useGame.ts` hook (central to game logic) contains:
        *   Mock Plinko game configuration and game logic (no API call for ball drop).
        *   `TODO`: Setup game-specific listeners for the Crash game.
        *   `TODO`: Implement actual cash-out logic (socket.emit or API call).
        *   `TODO`: Implement a separate start action post-bet if required by a game.
    *   `MinesGamePage.tsx` (example, likely similar for other specific game pages relying on `useGame` or direct mocks):
        *   Uses mock responses for starting a game, revealing tiles, and cashing out.
        *   `TODO`: Fetch full Provably Fair (PF) data for verification on game over.

*   **Lobby (`GameLobbyPage.tsx` vs `GamesLobbyPage.tsx`):**
    *   Ambiguity exists with two lobby pages:
        *   `GamesLobbyPage.tsx`: Simpler, static, and currently routed for `/games`.
        *   `GameLobbyPage.tsx`: More dynamic (fetching from `gameService`, search, filtering placeholders), seems less complete/polished (e.g., provider filtering UI missing, `getProviders` call commented out in service) but is referenced by `GameCard` and `gameService` for types.
    *   This suggests `GameLobbyPage.tsx` might be a newer version under development or a refactor target, while the simpler `GamesLobbyPage.tsx` acts as the current live version.

*   **Wallet (`WalletDashboardPage.tsx`, and components like `ActiveBonuses.tsx`):**
    *   `WalletDashboardPage.tsx` has a `TODO`: Add calls to fetch game history and active bonuses (when those stores/slices are ready).
    *   `ActiveBonuses.tsx` (used in the dashboard) uses mock data for active bonuses and has a `TODO` to replace it with an API call.

*   **Authentication (`LoginForm.tsx`, `RegistrationForm.tsx`):**
    *   These forms use `authService.login` and `authService.register` respectively, which appear to point to actual service implementations. No explicit "mock" or "TODO" for the form submission itself, but functionality depends on the backend and `authService`.

*   **Unit/Integration Tests (various `*.test.tsx?` files):**
    *   Many test files (e.g., `DiceGame.test.tsx`, `useGame.test.ts`) use extensive mocking for hooks (e.g., `useGame`, `walletSlice`), services (`apiClient`, `socketService`), and component dependencies. This is typical for testing but highlights areas where real integrations are abstracted away in tests.

*   **Informational Pages - Placeholders & Potential Contradictions:**
    *   **`ProvablyFairInfoPage.tsx`:** Contains a commented-out placeholder for a general Provably Fair verifier tool/link, which differs from the current game-specific verifier integration found on game pages.
    *   **`PaymentMethodsInfoPage.tsx`:**
        *   Uses a potential placeholder for `MoneroIcon` with a comment `// Assuming a MoneroIcon component exists or will be created`.
        *   Crucial transaction details (min/max deposit/withdrawal, fees, estimated times) are explicitly placeholders within a static array (`transactionDetails`), marked with `// Placeholder data ... this could be dynamic from config/API if needed`. Some values have inline comments like `(per transaction, higher limits may be available)` or `(Example fee)`, indicating the displayed information could be inaccurate.
    *   General note: Many informational pages present static content. While not explicitly "mocked" in a code sense, the accuracy of this information (e.g., specific terms in `TermsAndConditionsPage.tsx`, advice in `ResponsibleGamblingPage.tsx`) would need to be verified against actual operational policies, which is beyond a code review for TBD/mocked *functionality* but important for overall site integrity. 
