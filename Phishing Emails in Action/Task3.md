# Task 3: Track Your Package - Full Email Analysis
**Status:** Complete

### Sample Overview
Analyzed a fake shipping notification email. Attacker mimicked "Distribution Center" to create urgency. 
Subject: `Track your package: # LZ8942357486EN` - fake tracking number used to trigger curiosity.

### Initial Observations
**Red Flags Found:**
1. **Subject Line**: Fake tracking number `LZ8942357486EN` used to create urgency. 
   Psychology: "Mera parcel hai kya?" - user bina soche click karega.

2. **From Address Spoofing**: 
   Display name: `Distribution Center`  looks legit
   Actual email: `contact@beginpro.club`  red flag
   Real courier companies kabhi `.club` domain use nahi karte. Ye immediate mismatch hai.

3. **Technique Used**: Spoofed sender + urgency tactics. Attacker trusted brand copy kar raha hai.

### HTML Source + Link Analysis
Raw email source check karke pata chala attacker kya chupa raha tha:

```html
<a href="http://devret.xyz/4833mt11254939vf6888zq22032si1269du1508rr">
  Track your package: # LZ8942357486EN
</a>

