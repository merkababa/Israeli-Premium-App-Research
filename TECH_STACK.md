# Technology Stack Strategy

To keep the initial budget low and maximize time-to-market, the strategy focuses on a single codebase that deploys to iOS, Android, and Web simultaneously, leveraging BaaS (Backend as a Service) for infrastructure.

## Frontend (Web & Mobile)
- **Framework:** React Native with Expo (or alternatively, Flutter).
- **Reasoning:** Allows building the app and the web version simultaneously with one codebase. Expo provides rapid development and easy over-the-air updates.
- **Styling:** NativeWind (Tailwind for React Native) or standard StyleSheet for highly polished, premium UI.

## Backend & Database
- **Platform:** Supabase or Firebase.
- **Reasoning:** Both offer generous free tiers, out-of-the-box authentication, fast database setup, and real-time capabilities without needing a dedicated backend developer for the MVP.
- **Database:** PostgreSQL (if Supabase) or NoSQL (if Firebase Firestore).

## Payments
- **Gateway:** Stripe.
- **Reasoning:** Fully supports Israel, Apple Pay, and Google Pay. Essential for the MVP to provide frictionless checkout.
- **Future Integration:** Bit or PayBox via a local gateway, as they are dominant in Israel for P2P and increasingly for B2C, but Apple/Google Pay via Stripe is sufficient for launch.

## AI Integration
- **Service:** OpenAI API (GPT-4o or similar).
- **Reasoning:** Power a smart concierge chatbot that helps users find the exact service they need using natural language. Easy to integrate via REST API.
