# 🏃‍♂️ Apple Health to TCX Converter

Convert Apple Watch workouts from Apple Health export to TCX format for importing to Garmin Connect and other fitness platforms.

## ✨ Features

- 🔄 Converts Apple Watch workouts to industry-standard TCX format
- 📍 Preserves GPS routes, heart rate data, and workout statistics
- 📁 Organises workouts by year/month for easy management
- 💓 Separates workouts with and without heart rate data
- 🏃‍♀️ Supports running, walking, cycling, and other workout types

## 📋 Requirements

- 🐍 Python 3.6+
- 📱 Apple Health export data

## 📤 How to Export Apple Health Data

1. **Open the Apple Health app** on your iPhone
2. **Tap your profile picture** (top right corner)
3. **Scroll down and tap "Export All Health Data"**
4. **Tap "Export"** to confirm
5. **Choose how to share** the export file (AirDrop to Mac, email, etc.)
6. **Extract the ZIP file** - you'll get a folder containing:
   - `export.xml` - Main health data including workout statistics
   - `export_cda.xml` - Clinical data (not needed)
   - `workout-routes/` - Folder with GPX files for each workout
   - `electrocardiograms/` - ECG data (if available)

## 🚀 Usage

1. **Clone this repository:**
   ```bash
   git clone https://github.com/brtkwr/apple-health-tcx-converter.git
   cd apple-health-tcx-converter
   ```

2. **Run the converter:**
   ```bash
   python3 convert_apple_workouts.py /path/to/your/apple_health_export
   ```

3. **Optional: Filter by activity type:**
   ```bash
   python3 convert_apple_workouts.py /path/to/export --activity running
   python3 convert_apple_workouts.py /path/to/export --activity walking
   ```

4. **Optional: Specify output directory:**
   ```bash
   python3 convert_apple_workouts.py /path/to/export --output /path/to/tcx/files
   ```

## 📂 Output Structure

The script creates the following folder structure:

```
tcx_files/
├── 2022/
│   ├── 01/
│   │   ├── 2022-01-15_143022_Running.tcx
│   │   └── 2022-01-20_091505_Walking.tcx
│   └── 02/
│       └── 2022-02-03_182330_Running.tcx
├── 2023/
│   └── ...
└── no_heart_rate/
    └── 2022/
        └── 01/
            └── 2022-01-10_120000_Walking.tcx
```

## 🔄 What Gets Converted

### ✅ Workouts WITH Heart Rate Data
- Complete TCX files with GPS coordinates and heart rate for each trackpoint
- Workout statistics (average/min/max heart rate, distance, calories, duration)
- Compatible with Garmin Connect, Strava, TrainingPeaks, etc.

### ⚠️ Workouts WITHOUT Heart Rate Data
- TCX files with GPS coordinates only (no heart rate data)
- Stored in separate `no_heart_rate/` folder
- Still useful for route and distance tracking

## 📊 Importing to Garmin Connect

1. **Go to [Garmin Connect](https://connect.garmin.com)**
2. **Click the "+" button** → Import Data
3. **Upload your TCX files** (can select multiple files)
4. **Wait for processing** - workouts will appear in your timeline

## ⚙️ Technical Details

### Supported Data
- **GPS coordinates** (latitude, longitude, altitude)
- **Heart rate statistics** (average, minimum, maximum)
- **Workout metrics** (distance, duration, calories, elevation gain)
- **Activity types** (Running, Walking, Cycling, Swimming, Other)
- **Timestamps** (preserved from original workout)

### File Format
The script generates TCX (Training Center XML) files compatible with:
- Garmin Connect
- Strava
- TrainingPeaks
- Golden Cheetah
- Most other fitness platforms

### Heart Rate Data
Apple Health exports contain workout-level heart rate statistics (avg/min/max) but not second-by-second heart rate data. The converter applies the average heart rate to all trackpoints for Garmin Connect compatibility.

## 🔧 Troubleshooting

**"Found 0 Apple Watch workouts"**
- Make sure you've exported from the Apple Health app (not Apple Watch app)
- Verify the export folder contains `export.xml` and `workout-routes/` folder

**"No heart rate data"**
- Early Apple Watch workouts may not have recorded heart rate
- These are saved separately in the `no_heart_rate/` folder
- They can still be imported for GPS and distance data

**Large export files**
- The script processes workouts in batches
- For very large exports, consider filtering by year or activity type

## 🤝 Contributing

Feel free to open issues or submit pull requests to improve the converter.

## 📄 License

MIT License - feel free to use and modify as needed.