# CiviFix - Crowd-Sourced Civic Issues Management System

CiviFix is a modern web application that enables citizens to report civic issues in their community by taking photos. The system uses YOLOv8 AI-powered detection to automatically classify issues like garbage, potholes, and broken streetlights.

## 🌟 Features

- **📸 Real-time Camera Capture**: Take photos directly from your device's camera with live preview
- **📍 GPS Location Auto-detection**: Automatically captures and displays your current location
- **🤖 YOLOv8 AI Detection**: Automatic classification of civic issues using YOLOv8 algorithm
- **🗂️ Issue Types Supported**:
  - 🗑️ Garbage/Trash
  - 🕳️ Potholes
  - 💡 Broken Streetlights
- **📊 Public Feed**: View all reported issues in a beautiful card-based layout
- **👨‍💼 Admin Dashboard**: Manage report statuses (Open → In Progress → Resolved)
- **📱 Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Git

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone <YOUR_GIT_URL>
   cd civifix
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:5173`

## 🔧 Configuration

### Connecting Your YOLOv8 Detection API

The application is designed to work with an external YOLOv8-based detection service. To connect your API:

1. Navigate to your backend settings
2. Add a secret called `AI_DETECT_ENDPOINT` with your API URL (e.g., `https://your-yolo-api.com`)
3. Your API should expose a `/detect` endpoint that:
   - Accepts: `multipart/form-data` with an `image` field
   - Returns: JSON with `issue_type` (string) and `confidence` (number 0-1)

**Example API Response:**
```json
{
  "issue_type": "Pothole",
  "confidence": 0.92
}
```

### Without External API

If no `AI_DETECT_ENDPOINT` is configured, the system uses mock detection for demonstration purposes.

## 📁 Project Structure

```
civifix/
├── src/
│   ├── components/
│   │   ├── CameraCapture.tsx    # Real-time camera interface
│   │   ├── DetectionResult.tsx  # AI detection result display
│   │   ├── Header.tsx           # Navigation header
│   │   ├── ImageUploader.tsx    # Image upload with camera/file options
│   │   ├── LocationDisplay.tsx  # GPS location component
│   │   └── ReportCard.tsx       # Issue card for feed
│   ├── hooks/
│   │   ├── useCamera.ts         # Camera capture hook
│   │   └── useLocation.ts       # GPS location hook
│   ├── pages/
│   │   ├── Index.tsx            # Main report submission page
│   │   ├── Feed.tsx             # Public issues feed
│   │   └── Admin.tsx            # Admin dashboard
│   ├── lib/
│   │   └── api.ts               # API functions
│   └── types/
│       └── report.ts            # TypeScript interfaces
├── supabase/
│   └── functions/
│       └── detect-issue/        # Edge function for detection
└── README.md
```

## 🛠️ Tech Stack

- **Frontend**: React 18, TypeScript, Vite
- **Styling**: Tailwind CSS, shadcn/ui components
- **Backend**: Supabase (Database, Storage, Edge Functions)
- **AI**: YOLOv8 integration via REST API
- **Location**: Browser Geolocation API + OpenStreetMap Nominatim

## 📱 Usage Guide

### Reporting an Issue

1. Open the app and allow location access when prompted
2. Click **"Take Photo"** to use your camera, or drag & drop an image
3. The app will:
   - Capture your GPS coordinates
   - Upload the image
   - Send it to the YOLOv8 detection API
   - Display the detected issue type and confidence
4. Your report is automatically saved and visible in the public feed

### Viewing Reports

- Navigate to **Public Feed** to see all reported issues
- Issues are color-coded:
  - 🟢 Green: Garbage
  - 🟠 Orange: Pothole  
  - 🟡 Yellow: Broken Streetlight

### Managing Reports (Admin)

1. Navigate to the **Admin** dashboard
2. View all reports in a table format
3. Update status: Open → In Progress → Resolved

## 🔒 Security

- All data is stored securely in Supabase
- Images are stored in a public bucket for display
- Row-Level Security (RLS) policies protect database operations

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -m 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Open a Pull Request

## 📄 License

This project is open source and available under the MIT License.

## 🆘 Support

For issues or questions:
- Open a GitHub issue
- Check the documentation at [Lovable Docs](https://docs.lovable.dev)

---

Built with ❤️ using [Lovable](https://lovable.dev)
