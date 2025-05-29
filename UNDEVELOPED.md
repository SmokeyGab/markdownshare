## Frontend TBD/Mocked Features (Comprehensive Page Review)

Based on a review of frontend page components (`frontend/casinoxmr-app/src`), the following features are currently using mock data, are marked as TBD/TODO, or have unimplemented functionalities. Each item includes a high-level relative effort estimation to complete or address it.

*   **Content - Game Guides (`GameGuideDetailPage.tsx`, `GameGuidesListPage.tsx`):**
    *   Data fetching for game guides uses mock data (`mockGameGuidesFull`, `mockGameGuides`).
        *   **Relative Effort Estimation:** Medium. Requires defining a data source/CMS, backend API endpoints (if not using static files), and frontend service integration for fetching and parsing guide content.
    *   Explicit `TODO` comments to replace mock data with actual data fetching strategies.
        *   **Relative Effort Estimation:** (Covered by the point above).
    *   `GameGuidesListPage.tsx` has a `TODO` to add filtering/search functionality.
        *   **Relative Effort Estimation:** Small to Medium. UI components for filters/search are straightforward. Complexity depends on whether filtering logic is client-side (if all guides are loaded) or requires backend support.

*   **Content - Blog (`BlogListPage.tsx`, `BlogPostPage.tsx`):**
    *   Data fetching for blog posts and individual post content uses mock data (`mockBlogPosts`, `mockBlogPostsFull`).
        *   **Relative Effort Estimation:** Medium. Similar to Game Guides; requires a content source (CMS, markdown files), potential backend API, and frontend service integration.
    *   Explicit `TODO` comments to replace mock data with actual data fetching (e.g., API call or markdown parsing).
        *   **Relative Effort Estimation:** (Covered by the point above).
    *   `BlogListPage.tsx` has a `TODO` to add pagination.
        *   **Relative Effort Estimation:** Small. If data fetching is in place, adding pagination UI and logic (client or server-side) is generally a minor task.

*   **Affiliate Program (`AffiliateProgramPage.tsx`):**
    *   Affiliate registration (`handleAffiliateRegister`) and login (`handleAffiliateLogin`) functionalities are placeholders (show alerts). Actual implementation of forms/modals or navigation to a portal is pending.
        *   **Relative Effort Estimation:** Large. This likely involves significant backend work (affiliate tracking, commission logic, database changes) and corresponding frontend UI for registration, login, and an affiliate dashboard (which isn't explicitly mentioned but implied).

*   **Promotions (`PromotionsPage.tsx`):**
    *   Fetches promotions using mock data (`mockPromotions`).
        *   **Relative Effort Estimation:** Medium. Requires backend API endpoints for fetching available and user-specific promotions, and frontend service integration.
    *   `useEffect` and `handleClaimPromotion` simulate API calls, with comments indicating they need to be replaced with real API calls.
        *   **Relative Effort Estimation:** Small to Medium. Frontend part involves updating service calls. Backend needs to handle promotion claiming logic.

*   **Info - Contact Us (`ContactUsPage.tsx`):**
    *   Contact form submission (`handleSubmit`) is simulated (logs to console, shows alert). Actual backend integration is pending.
        *   **Relative Effort Estimation:** Small to Medium. Frontend form is mostly there. Requires a backend endpoint (e.g., to send an email or store submissions) and wiring it up.
    *   Placeholder email address `support@casinoxmr.example.com`.
        *   **Relative Effort Estimation:** Trivial. Requires updating a string literal once the actual email is known.
    *   Live Chat feature is commented out and marked "Coming Soon".
        *   **Relative Effort Estimation:** Medium to Large. Integrating a third-party live chat service or building a custom one involves frontend UI and potentially backend/webhook integrations.
    *   FAQ data is static; might be intended to be dynamic in a full implementation.
        *   **Relative Effort Estimation:** Small to Medium. If dynamic content is desired, it needs a data source (CMS, simple JSON file, API) and frontend logic to fetch and render.

*   **Home Page (`HomePage.tsx`):**
    *   Uses placeholder data for `featuredGames` and `currentPromotion` (comment indicates this should come from API/state).
        *   **Relative Effort Estimation:** Medium. Requires backend APIs to define/fetch featured games and current promotions, and frontend integration to display this dynamic content.
    *   Uses placeholder image paths that need to be replaced with actual assets.
        *   **Relative Effort Estimation:** Small. Involves obtaining the actual image assets and updating paths in the code/CMS.

*   **Games - General (affecting all game pages like `DiceGamePage.tsx`, `MinesGamePage.tsx`, etc., primarily through `useGame.ts`):**
    *   The `useGame.ts` hook (central to game logic) contains:
        *   Mock Plinko game configuration and game logic (no API call for ball drop).
            *   **Relative Effort Estimation:** Medium to Large (per game type). Plinko, specifically, needs backend logic for ball drop physics/outcome determination if it's to be server-authoritative, and frontend to integrate with this.
        *   `TODO`: Setup game-specific listeners for the Crash game.
            *   **Relative Effort Estimation:** Medium (per game type). Crash game requires real-time WebSocket communication for the multiplier and game state, involving both frontend and backend work.
        *   `TODO`: Implement actual cash-out logic (socket.emit or API call).
            *   **Relative Effort Estimation:** Medium. Backend needs to handle cash-out requests securely for each game, update user balances, and manage game state. Frontend needs to make these calls.
        *   `TODO`: Implement a separate start action post-bet if required by a game.
            *   **Relative Effort Estimation:** Small to Medium (per game type, if applicable). Depends on game design; some games might combine bet and start, others might separate them. Involves frontend UI changes and backend logic.
    *   `MinesGamePage.tsx` (example, likely similar for other specific game pages relying on `useGame` or direct mocks):
        *   Uses mock responses for starting a game, revealing tiles, and cashing out.
            *   **Relative Effort Estimation:** (Largely covered by the `useGame.ts` points above, as these actions would go through the hook). If a game doesn't use `useGame` and has its own mocks, then Medium per game for backend logic and frontend integration.
        *   `TODO`: Fetch full Provably Fair (PF) data for verification on game over.
            *   **Relative Effort Estimation:** Small to Medium. Backend needs to expose all necessary PF data (unhashed server seed, client seed, nonce) post-game. Frontend needs to display it, potentially in the existing PF verifier component.

*   **Lobby (`GameLobbyPage.tsx` vs `GamesLobbyPage.tsx`):**
    *   Ambiguity exists with two lobby pages:
        *   `GamesLobbyPage.tsx`: Simpler, static, and currently routed for `/games`.
        *   `GameLobbyPage.tsx`: More dynamic (fetching from `gameService`, search, filtering placeholders), seems less complete/polished (e.g., provider filtering UI missing, `getProviders` call commented out in service) but is referenced by `GameCard` and `gameService` for types.
    *   This suggests `GameLobbyPage.tsx` might be a newer version under development or a refactor target, while the simpler `GamesLobbyPage.tsx` acts as the current live version.
        *   **Relative Effort Estimation for Resolution:** Medium. Decision needed on which lobby to proceed with. If `GameLobbyPage.tsx` is chosen:
            *   Complete provider filtering (backend API, frontend UI & logic): Small to Medium.
            *   Polish UI, ensure all features (search, sort, pagination) work correctly with backend: Medium.
            *   Switch routing in `App.tsx`: Trivial.

*   **Wallet (`WalletDashboardPage.tsx`, and components like `ActiveBonuses.tsx`):**
    *   `WalletDashboardPage.tsx` has a `TODO`: Add calls to fetch game history and active bonuses (when those stores/slices are ready).
        *   **Relative Effort Estimation:** Medium. Requires backend APIs for game history (likely with pagination/filters) and user's active/claimable bonuses. Frontend needs service integration and UI updates in respective components/stores.
    *   `ActiveBonuses.tsx` (used in the dashboard) uses mock data for active bonuses and has a `TODO` to replace it with an API call.
        *   **Relative Effort Estimation:** (Covered by the point above, as it's part of fetching active bonuses).

*   **Authentication (`LoginForm.tsx`, `RegistrationForm.tsx`):**
    *   These forms use `authService.login` and `authService.register` respectively, which appear to point to actual service implementations. No explicit "mock" or "TODO" for the form submission itself, but functionality depends on the backend and `authService`.
        *   **Relative Effort Estimation:** Low (assuming backend is functional). Work here is mostly about ensuring robustness, error handling, and UI polish if needed, rather than core implementation.

*   **Unit/Integration Tests (various `*.test.tsx?` files):**
    *   Many test files (e.g., `DiceGame.test.tsx`, `useGame.test.ts`) use extensive mocking for hooks (e.g., `useGame`, `walletSlice`), services (`apiClient`, `socketService`), and component dependencies. This is typical for testing but highlights areas where real integrations are abstracted away in tests.
        *   **Relative Effort Estimation:** Ongoing (Medium to Large overall). As features are unmocked and backend integrations are completed, corresponding tests will need to be updated or rewritten to reflect real interactions rather than mocked ones. This is an ongoing effort alongside development.

*   **Informational Pages - Placeholders & Potential Contradictions:**
    *   **`ProvablyFairInfoPage.tsx`:** Contains a commented-out placeholder for a general Provably Fair verifier tool/link, which differs from the current game-specific verifier integration found on game pages.
        *   **Relative Effort Estimation:** Small to Medium. Decide if a general tool page is needed. If so, create the page and link. If not, remove the comment. The existing game-specific verifier might be sufficient.
    *   **`PaymentMethodsInfoPage.tsx`:**
        *   Uses a potential placeholder for `MoneroIcon` with a comment `// Assuming a MoneroIcon component exists or will be created`.
            *   **Relative Effort Estimation:** Trivial. Create or verify the `MoneroIcon` component, or replace with a suitable existing icon/SVG.
        *   Crucial transaction details (min/max deposit/withdrawal, fees, estimated times) are explicitly placeholders within a static array (`transactionDetails`), marked with `// Placeholder data ... this could be dynamic from config/API if needed`. Some values have inline comments like `(per transaction, higher limits may be available)` or `(Example fee)`, indicating the displayed information could be inaccurate.
            *   **Relative Effort Estimation:** Small to Medium. If these values need to be dynamic, backend API endpoints are required. Frontend needs to fetch and display them. If they are to remain static for now, they simply need to be updated with correct, non-placeholder values.
    *   General note: Many informational pages present static content. While not explicitly "mocked" in a code sense, the accuracy of this information (e.g., specific terms in `TermsAndConditionsPage.tsx`, advice in `ResponsibleGamblingPage.tsx`) would need to be verified against actual operational policies, which is beyond a code review for TBD/mocked *functionality* but important for overall site integrity. 
        *   **Relative Effort Estimation:** Small (for content updates). This is primarily a content management/review task, not a coding task, unless the content needs to be fetched dynamically (which would be covered elsewhere). 
