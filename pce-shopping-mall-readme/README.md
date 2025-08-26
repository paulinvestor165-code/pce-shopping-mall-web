# 🛍️ PCE Shopping Mall  

A shopping mall app built with **React + Firebase**, including **Paystack payment integration**.  
Users can register as buyers or sellers, list products for sale, place orders, and track order status.  
The app supports different roles: **User, Seller, and Owner/Admin**.  

---

## ✨ Features
- 🔑 User Authentication (Signup, Login, Logout)  
- 👤 Role-based access: User, Seller, Owner/Admin  
- 🛒 Add, Edit, Delete Products (Sellers + Owner)  
- 💳 Paystack Integration with ₦200 commission added per order  
- 📦 Order Management:  
  - Buyers see their purchases  
  - Sellers see orders for their products  
  - Owner sees **all orders** across the platform  
- 🚚 Mark orders as *Delivered* (Sellers)  
- 📱 Mobile app version built with Expo (React Native)  

---

## 📂 Project Structure
```
pce-shopping-mall-both/
├── pce-shopping-mall-web/     # React web app (Netlify ready)
└── pce-shopping-mall-mobile/  # Expo React Native app
```

---

## ⚡ Setup (Web)
1. Clone or download this repo.  
2. Go inside the web project:  
   ```bash
   cd pce-shopping-mall-web
   ```
3. Install dependencies:  
   ```bash
   npm install
   ```
4. Add your Firebase config & Paystack public key in `src/App.js`.  
5. Run locally:  
   ```bash
   npm start
   ```
6. Build for production:  
   ```bash
   npm run build
   ```
7. Deploy to [Netlify Drop](https://app.netlify.com/drop) — drag the `build/` folder.

---

## ⚡ Setup (Mobile)
1. Go inside the mobile project:  
   ```bash
   cd pce-shopping-mall-mobile
   ```
2. Install dependencies:  
   ```bash
   npm install
   ```
3. Add Firebase config & Paystack public key in `App.js`.  
4. Start with Expo:  
   ```bash
   npx expo start
   ```
5. Scan QR with **Expo Go app** (Android/iOS).  

---

## 🔐 Firebase Firestore Rules
```js
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
```

---

## 🌐 Deployment
- **Web:** Netlify (recommended) or Firebase Hosting  
- **Mobile:** Expo (easy testing), later publish to Play Store / App Store  

---

## 📞 Support
- 📧 Email: **pceshoppingmall@gmail.com**  
- 📱 Phone: **+2347089724573**  
- ✅ Trustable and reliable shopping platform  
