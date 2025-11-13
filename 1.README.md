# ThirdEye_Bangladesh
# Third Eye - Bangladesh Traffic Safety App

![Third Eye Logo](https://images.unsplash.com/photo-1449965408869-eaa3f722e40d?w=400&h=200&fit=crop)

## 🎯 Overview

**Third Eye** is an official traffic safety reporting application for Bangladesh, developed in partnership with:
- **DMP** (Dhaka Metropolitan Police)
- **BRTA** (Bangladesh Road Transport Authority)

The app enables citizens to report traffic violations with photo evidence and earn rewards, while helping authorities maintain road safety.

---

## ✨ Features

### For Citizens
- ✅ **Report Traffic Violations** - Capture photo evidence with GPS location
- ✅ **Earn Rewards** - Get 20% of fine amount for verified reports
- ✅ **Track Reports** - View status of submitted violations
- ✅ **Search Cases** - Find reports by case number or vehicle
- ✅ **Emergency Contacts** - Quick dial Police, Ambulance, Fire
- ✅ **Bilingual** - Full support for English and Bengali

### For Officers (DMP/BRTA)
- ✅ **Verify Reports** - Review and approve/reject submissions
- ✅ **Issue E-Challans** - Digital violation notices
- ✅ **Case Management** - Track and manage violations
- ✅ **Dashboard Analytics** - View stats and reports

### Security Features
- ✅ **KYC Verification** - Mandatory identity verification
- ✅ **First Reporter Reward** - Prevents duplicate reporting
- ✅ **Penalty System** - Discourages false reports
- ✅ **Secure Authentication** - OAuth and session management

---

## 🚀 Quick Start for Non-Developers

### I Want to...

#### 📱 Publish to App Stores
**Read:** `MOBILE_PUBLISHING_GUIDE.md`
- Complete guide for Google Play Store
- Complete guide for Apple App Store
- PWA installation guide (easiest option)
- Step-by-step instructions with screenshots

#### 🎨 Create App Icons and Screenshots
**Read:** `ASSET_CREATION_GUIDE.md`
- What images you need
- Required sizes for each platform
- How to create them using free tools (Canva, Figma)
- Templates and examples

#### 🌐 Deploy Online
**Read:** `DEPLOYMENT_GUIDE.md`
- Deploy to Cloudflare (free)
- Set up database and storage
- Configure custom domain
- Automatic deployments

#### 📂 Understand the Code
**Read:** `FILE_STRUCTURE_GUIDE.md`
- What every file does
- What you can safely edit
- How everything connects
- Troubleshooting guide

---

## 📦 Project Structure

```
third-eye-app/
├── 📱 Mobile Guides/
│   ├── MOBILE_PUBLISHING_GUIDE.md    # Publish to Play Store & App Store
│   ├── ASSET_CREATION_GUIDE.md       # Create icons and screenshots
│   ├── DEPLOYMENT_GUIDE.md           # Deploy app online
│   └── FILE_STRUCTURE_GUIDE.md       # Understand the codebase
│
├── 💻 Source Code/
│   ├── src/react-app/                # Frontend (what users see)
│   │   ├── pages/                    # All app pages
│   │   ├── components/               # Reusable UI components
│   │   └── hooks/                    # App logic
│   ├── src/worker/                   # Backend API
│   └── src/shared/                   # Shared code
│
├── 🎨 Public Assets/
│   ├── manifest.json                 # PWA configuration
│   └── sw.js                        # Offline support
│
└── ⚙️ Configuration/
    ├── package.json                  # Dependencies
    ├── tailwind.config.js            # Styling
    └── wrangler.json                 # Deployment config
```

---

## 🎨 Design System

### Colors (DO NOT CHANGE)
```css
Primary Blue:    #3b82f6
Purple:          #9333ea  
Orange:          #f97316
Red:             #ef4444
Green:           #10b981
Gray Light:      #f9fafb
Gray Dark:       #1f2937
```

### Logo
- Eye icon (👁️) with blue background
- Rounded corners
- Used consistently across all pages

### Typography
- Mobile-optimized sizes
- High contrast for readability
- System fonts (San Francisco, Roboto)

---

## 📱 App Pages

### Public Pages (No Login Required)
1. **Home** - Welcome page with login/signup
2. **Login Portals** - Citizen, DMP, BRTA login
3. **Sign Up Portals** - Registration options

### Protected Pages (Login Required)
1. **Dashboard** - User stats and quick actions
2. **Report** - Submit violation with photo
3. **Search** - Find cases by number/vehicle
4. **KYC** - Identity verification
5. **Penalties** - View and pay fines
6. **Emergency** - Quick dial emergency numbers

### Officer Pages
1. **DMP Dashboard** - Verify reports, issue e-challans
2. **BRTA Dashboard** - Manage violations

---

## 🔧 Technical Stack

### Frontend
- **Framework:** React 18 with TypeScript
- **Routing:** React Router v6
- **Styling:** Tailwind CSS
- **Icons:** Lucide React
- **Build Tool:** Vite

### Backend
- **Runtime:** Cloudflare Workers
- **API Framework:** Hono
- **Database:** Cloudflare D1 (SQLite)
- **Storage:** Cloudflare R2
- **Authentication:** Mocha Users Service

### Mobile
- **PWA:** Progressive Web App (installable)
- **Responsive:** Mobile-first design
- **Offline:** Service worker caching

---

## 🚦 Getting Started (Developers)

### Prerequisites
- Node.js 20+ installed
- Git installed
- GitHub account
- Cloudflare account

### Installation

```bash
# 1. Clone repository
git clone https://github.com/yourusername/third-eye-app.git
cd third-eye-app

# 2. Install dependencies
npm install

# 3. Set up environment variables
cp .dev.vars.example .dev.vars
# Edit .dev.vars and add your API keys

# 4. Start development server
npm run dev

# 5. Open in browser
# Visit http://localhost:5173
```

### Database Setup

```bash
# Create D1 database
npx wrangler d1 create third-eye-db

# Run migrations
npx wrangler d1 migrations apply third-eye-db --local
```

### R2 Storage Setup

```bash
# Create R2 bucket
npx wrangler r2 bucket create third-eye-photos
```

---

## 📝 Available Scripts

```bash
# Development
npm run dev              # Start dev server with hot reload

# Building
npm run build            # Build for production
npm run preview          # Preview production build

# Deployment
npm run deploy           # Deploy to Cloudflare Workers

# Database
npx wrangler d1 migrations apply third-eye-db --local   # Local DB
npx wrangler d1 migrations apply third-eye-db --remote  # Production DB

# Testing
npm run type-check       # Check TypeScript types
npm run lint            # Run ESLint
```

---

## 🗄️ Database Schema

### Main Tables
- `users` - Citizen, DMP, BRTA accounts
- `reports` - All violation reports
- `dmp_officers` - DMP officer data
- `brta_officers` - BRTA officer data
- `penalties` - Fines for false reports
- `incident_races` - First reporter tracking
- `payments` - Payment transactions
- `payment_methods` - User payment accounts

---

## 🔐 Authentication Flow

1. User clicks "Start Reporting"
2. Redirected to OAuth provider (Google)
3. After auth, redirected to `/auth/callback`
4. Session created, user lands on `/onboarding`
5. Complete registration (user type, KYC, payment)
6. Access granted to dashboard

---

## 📊 Reward System

### How It Works
1. Citizen reports violation with photo + GPS
2. System checks if same incident already reported (5-min window, nearby location)
3. If first reporter: eligible for reward
4. If duplicate: recorded but no reward
5. DMP/BRTA officer verifies report
6. If approved: reward = 20% of fine amount
7. Reward credited to user's mobile wallet

### Violation Fines
```
Helmet Violation:        ৳500  → Reward: ৳100
Signal Jump:             ৳1000 → Reward: ৳200
Wrong Way:               ৳500  → Reward: ৳100
Overspeeding:            ৳1000 → Reward: ৳200
Mobile While Driving:    ৳1000 → Reward: ৳200
Triple Riding:           ৳500  → Reward: ৳100
Parking Violation:       ৳300  → Reward: ৳60
License Violation:       ৳2000 → Reward: ৳400
```

---

## 🚨 Emergency Contacts

Quick dial buttons for:
- **Police:** 999
- **Ambulance:** 199
- **Fire Service:** 101
- **DMP Control:** +88-02-9330524
- **BRTA Helpline:** 09612100100

---

## 🌍 Deployment

### Production Deployment (Cloudflare)

```bash
# 1. Login to Cloudflare
npx wrangler login

# 2. Deploy
npm run deploy

# 3. Set up database (first time)
npx wrangler d1 migrations apply third-eye-db --remote

# 4. Configure secrets
npx wrangler secret put MOCHA_USERS_SERVICE_API_KEY
npx wrangler secret put MOCHA_USERS_SERVICE_API_URL
```

### Custom Domain
1. Add domain to Cloudflare
2. Update nameservers
3. Wait for propagation (up to 24 hours)
4. Connect domain in Workers & Pages settings

---

## 🧪 Testing

### Test Accounts

**Citizen Account:**
- Email: `citizen@test.com`
- Password: `Test123!`

**DMP Officer:**
- Email: `dmp@test.com`
- Password: `Test123!`

**BRTA Officer:**
- Email: `brta@test.com`
- Password: `Test123!`

### Manual Testing Checklist

- [ ] Home page loads
- [ ] Language toggle works (EN/BN)
- [ ] Can login/signup
- [ ] Can complete registration
- [ ] Can upload KYC documents
- [ ] Can submit report with photo
- [ ] GPS location captures
- [ ] Can search by case number
- [ ] Can search by vehicle number
- [ ] Emergency contacts dial
- [ ] PWA installs on mobile
- [ ] Works offline (basic features)

---

## 🐛 Common Issues & Solutions

### Issue: "Cannot find module"
**Solution:** Run `npm install`

### Issue: "Database error"
**Solution:** Check D1 binding in wrangler.json

### Issue: "Image upload fails"
**Solution:** Verify R2 bucket exists and binding is correct

### Issue: "PWA won't install"
**Solution:** Must be served over HTTPS, check manifest.json

### Issue: "Location not working"
**Solution:** User must grant permission, use HTTPS

---

## 📚 Documentation

- [Mobile Publishing Guide](MOBILE_PUBLISHING_GUIDE.md) - Publish to app stores
- [Asset Creation Guide](ASSET_CREATION_GUIDE.md) - Create graphics
- [Deployment Guide](DEPLOYMENT_GUIDE.md) - Deploy online
- [File Structure Guide](FILE_STRUCTURE_GUIDE.md) - Understand codebase

---

## 🤝 Contributing

### For Developers
1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### Code Style
- Use TypeScript
- Follow existing patterns
- Mobile-first responsive
- Add comments for complex logic
- Test on multiple devices

---

## 📜 License

This project is proprietary software developed for Third Eye Bangladesh in partnership with DMP and BRTA.

---

## 📞 Support

### For Users
- **Email:** support@thirdeyebangladesh.com
- **Phone:** +880-XX-XXXXXXX
- **Website:** https://thirdeyebangladesh.com

### For Developers
- **Issues:** GitHub Issues
- **Discussions:** GitHub Discussions
- **Email:** dev@thirdeyebangladesh.com

---

## 🙏 Acknowledgments

- **Dhaka Metropolitan Police (DMP)** - Partnership and verification
- **Bangladesh Road Transport Authority (BRTA)** - Regulatory support
- **Citizens of Bangladesh** - Making roads safer together
- **Development Team** - Technical infrastructure and support

---

## 🎯 Roadmap

### Phase 1 (Current) ✅
- [x] Citizen reporting
- [x] KYC verification
- [x] Officer verification
- [x] Reward system
- [x] Emergency contacts

### Phase 2 (Planned) 🚧
- [ ] Mobile wallet integration (bKash, Nagad)
- [ ] Push notifications
- [ ] In-app payments
- [ ] Officer mobile app
- [ ] Advanced analytics

### Phase 3 (Future) 🔮
- [ ] AI violation detection
- [ ] Video evidence support
- [ ] Community forums
- [ ] Reward redemption marketplace
- [ ] Integration with traffic management systems

---

## 📊 Statistics (Projected)

- **Target Users:** 100,000+ citizens
- **Coverage:** All 92 districts of Bangladesh
- **Partners:** DMP, BRTA, Local Police
- **Languages:** English, Bengali
- **Platform:** Web, Android, iOS

---

## 🌟 Star History

If you find this project useful, please consider giving it a star on GitHub! ⭐

---

## 📱 Download Links (After Publishing)

- **Google Play Store:** Coming Soon
- **Apple App Store:** Coming Soon  
- **Web App:** https://thirdeyebangladesh.com

---

**Made with ❤️ in Bangladesh for a Safer Tomorrow**

*Developed by an independent development team committed to road safety.*

---

## Quick Navigation

- [Overview](#-overview)
- [Features](#-features)
- [Quick Start](#-quick-start-for-non-developers)
- [Installation](#-getting-started-developers)
- [Documentation](#-documentation)
- [Support](#-support)
