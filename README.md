🛍️ PCE Shopping Mall
A shopping mall app built with React + Firebase, including Paystack payment integration.
Users can register as buyers or sellers, list products for sale, place orders, and track order status.
The app supports different roles: User, Seller, and Owner/Admin.

✨ Features
🔑 User Authentication (Signup, Login, Logout)
👤 Role-based access: User, Seller, Owner/Admin
🛒 Add, Edit, Delete Products (Sellers + Owner)
💳 Paystack Integration with ₦200 commission added per order
📦 Order Management:
Buyers see their purchases
Sellers see orders for their products
Owner sees all orders across the platform
🚚 Mark orders as Delivered (Sellers)
📱 Mobile app version built with Expo (React Native)
📂 Project Structure
pce-shopping-mall-both/
├── pce-shopping-mall-web/     # React web app (Netlify ready)
└── pce-shopping-mall-mobile/  # Expo React Native app
⚡ Setup (Web)
Clone or download this repo.
Go inside the web project:
cd pce-shopping-mall-web
Install dependencies:
npm install
Add your Firebase config & Paystack public key in src/App.js.
Run locally:
npm start
Build for production:
npm run build
Deploy to Netlify Drop — drag the build/ folder.
⚡ Setup (Mobile)
Go inside the mobile project:
cd pce-shopping-mall-mobile
Install dependencies:
npm install
Add Firebase config & Paystack public key in App.js.
Start with Expo:
npx expo start
Scan QR with Expo Go app (Android/iOS).
🔐 Firebase Firestore Rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /products/{productId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow update, delete: if request.auth != null && (
        request.auth.token.email == resource.data.owner ||
        request.auth.token.email == "owner@pceshoppingmall.org"
      );
    }
    match /orders/{orderId} {
      allow read, write: if request.auth != null && request.auth.token.email == "owner@pceshoppingmall.org";
      allow read, create: if request.auth != null && request.auth.token.email == request.resource.data.buyer;
      allow read: if request.auth != null && request.auth.token.email == resource.data.seller;
    }
  }
}
🌐 Deployment
Web: Netlify (recommended) or Firebase Hosting
Mobile: Expo (easy testing), later publish to Play Store / App Store
📞 Support
📧 Email: pceshoppingmall@gmail.com
📱 Phone: +2347089724573
✅ Trustable and reliable shopping platform
