# Setting up Pinata for IPFS Storage

Follow these steps to use Pinata's IPFS service with the DeNews application:

## Step 1: Create a Pinata Account
1. Go to [https://app.pinata.cloud/register](https://app.pinata.cloud/register)
2. Sign up for a free account (no credit card required)
3. Verify your email address

## Step 2: Generate a JWT Token
1. Go to your [Pinata Developer Dashboard](https://app.pinata.cloud/developers/api-keys)
2. Locate your existing API key "nftmarket" with key "4433335ab248718a461c"
3. Click on this API key to view its details
4. Look for the "Create JWT" button and click it
5. Make sure these permissions are enabled:
   - All files/pinning related endpoints
6. Click "Create JWT"
7. Copy the generated JWT token (it's a long string starting with "ey...")

## Step 3: Update Your Code with JWT
1. Open `client/src/components/AuthorPanel.js`
2. Find this line (around line 10):
```javascript
pinataJwt: "YOUR_PINATA_JWT_HERE", // Replace with your JWT
```
3. Replace it with your actual JWT token:
```javascript
pinataJwt: "eyJhbGci...YOUR_ACTUAL_JWT_TOKEN_HERE...", 
```

## Step 4: Configure CORS Settings (if needed)
1. In your [Pinata Developer Dashboard](https://app.pinata.cloud/developers/api-keys), click on the "CORS" tab
2. Add the following origins to allow uploads from your application:
   - `http://localhost:3000` (for local development)
   - Add any production domains if you deploy your app

## Step 5: Verify Your Gateway
1. Go to the [Gateways page](https://app.pinata.cloud/gateway)
2. Note your gateway domain (e.g., "jade-electronic-puma-736.mypinata.cloud")
3. Make sure it matches the one in the AuthorPanel.js file:
```javascript
const PINATA_GATEWAY = "jade-electronic-puma-736.mypinata.cloud";
```
4. If it doesn't match, update it with your gateway domain

## Step 6: Start Your Application
1. Run the application with `npm start` from the client directory
2. When uploading files, the app will use your JWT token to authenticate with Pinata

## Accessing Your Files
After uploading, your files will be available at:
- `https://jade-electronic-puma-736.mypinata.cloud/ipfs/YOUR_FILE_CID` (your dedicated gateway)
- Or any other public IPFS gateway, such as `https://ipfs.io/ipfs/YOUR_FILE_CID`

## Free Tier Limitations
Pinata's free tier includes:
- 500 Pinned Files
- 1GB Storage
- 1 Gateway
- 10G Bandwidth per month
- 10k Requests per month

This is enough for testing and small applications.

## Troubleshooting
If you encounter upload issues:
1. Check your browser console for error messages
2. Verify your JWT token is correct and not expired
3. Make sure CORS settings are correctly configured
4. Ensure your gateway domain is correct in the code

For more information, visit [Pinata's documentation](https://docs.pinata.cloud/) 