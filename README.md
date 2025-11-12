# MyAttendance - Smart Attendance Tracker

A Python desktop application designed to help students manage their attendance and calculate safe class skips while maintaining the 75% attendance threshold.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Tkinter](https://img.shields.io/badge/GUI-Tkinter-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## ✨ Why MyAttendance?

Stop worrying about attendance! MyAttendance is your personal attendance assistant that:
- ✅ Automatically tracks your presence (mark absences only!)
- � Shows real-time attendance percentage
- 🎯 Calculates exactly how many classes you can safely skip
- 🗓️ Provides a beautiful Google Calendar-like interface
- 🚀 Works completely offline with no internet required

## �📋 Features

### 🎯 Core Features
- **Google Calendar-Style Interface**: Monthly grid view with intuitive color-coded days
- **Smart Attendance Tracking**: All classes marked present by default, click to mark absent
- **75% Threshold Calculator**: Real-time calculation of safe classes to skip
- **Batch-Aware Timetable**: Supports B1/B3 and B2/B4 batch lab schedules
- **Holiday Management**: Mark individual days or date ranges as holidays
- **Data Persistence**: All data stored locally in JSON format
- **Reset Functionality**: Clear all data for new semester with one click

### 🖱️ Interaction Methods
- **Left-Click**: Select a date to mark individual subjects absent/present
- **Right-Click**: Instantly mark all classes for a day as absent
- **Holiday Toggle**: Single-click button to mark days as holidays

### 📊 Dashboard & Reports
- Real-time attendance statistics for all subjects
- Visual indicators (Green = Safe ≥75%, Red = At Risk <75%)
- Export detailed attendance reports to text files
- Quick stats: Total subjects, average attendance, at-risk count

## � Screenshots

### Main Interface
```
┌─────────────────────────────────────────────────────────┐
│  🎓 MyAttendance - Smart Attendance Tracker            │
├─────────────────────────────────────────────────────────┤
│  ⚙️ Setup  │  📋 Timetable  │  📅 Mark Attendance  │  📊 Summary │
├─────────────────────────────────────────────────────────┤
│                                                          │
│     November 2025                          [Prev] [Today] [Next]
│   ┌────┬────┬────┬────┬────┬────┬────┐                │
│   │Mon │Tue │Wed │Thu │Fri │Sat │Sun │                │
│   ├────┼────┼────┼────┼────┼────┼────┤                │
│   │ 🟢 │ 🟢 │ 🔴 │ 🟢 │ 🟡 │ ⚪ │ ⚪ │    Selected: Nov 15
│   │  1 │  2 │  3 │  4 │  5 │  6 │  7 │    ──────────────
│   ├────┼────┼────┼────┼────┼────┼────┤    ✓ DAA
│   │ 🟢 │ 🟢 │ 🟢 │ 🟢 │ 🔵 │ ⚪ │ ⚪ │    ✓ TOC
│   │  8 │  9 │ 10 │ 11 │ 12 │ 13 │ 14 │    ✗ CN (Absent)
│   └────┴────┴────┴────┴────┴────┴────┘    ✓ DM
│                                             
│   Legend: 🟢 Present │ 🔴 Absent │ 🟡 Holiday │ 🔵 Today
└─────────────────────────────────────────────────────────┘
```

## �🚀 Getting Started

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Windows/Mac/Linux (cross-platform compatible!)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/MyAttendance.git
cd MyAttendance
```

2. **Install dependencies**
```bash
pip install tkcalendar
```

3. **Run the application**
```bash
python app.py
```

## 📖 User Guide

### First-Time Setup
1. Launch the application
2. Select your batch (B1/B3 or B2/B4)
3. The app will automatically initialize all subjects from the timetable

### Setup Tab ⚙️
- **Batch Selection**: Choose between B1/B3 or B2/B4
- **Semester Dates**: Set start and end dates using calendar widgets
- **Holiday Management**: Add/remove holiday periods with names
- **Reset Data**: Clear all holidays and absent dates (preserves batch and semester dates)

### Timetable Tab 📋
- View your weekly schedule in a color-coded grid
- Theory classes (Blue), Lab sessions (Purple), Others (Orange)
- Shows correct labs based on your batch selection
- Read-only display for reference

### Mark Attendance Tab 📅
- **Monthly Calendar View**: Navigate using Prev/Next/Today buttons
- **Color-Coded Days**:
  - 🟢 Light Green: All classes present
  - 🔴 Light Red: Some classes marked absent
  - 🟡 Light Yellow: Holiday
  - 🔵 Light Blue: Today
  - ⚪ Light Gray: Weekend/Future dates

#### Marking Attendance
1. **Individual Subjects**:
   - Left-click any date
   - View subjects in side panel
   - Uncheck subjects to mark absent
   - Click "Save Attendance"

2. **Entire Day**:
   - Right-click any date
   - Confirms marking all classes as absent
   - No need to select individual subjects

3. **Holidays**:
   - Left-click a date
   - Click "🏖️ Mark as Holiday" button
   - Toggle back to regular day anytime

### Summary Tab 📊
- View all subjects with attendance percentages
- Columns: Subject | Present | Total | Attendance % | Status | Safe to Skip
- Quick stats cards showing overall performance
- Export detailed reports with timestamp

## 📁 Project Structure

```
MyAttendance/
├── 📄 app.py                  # Main entry point (window setup, tabs)
├── 📊 data_manager.py         # Timetable data, JSON persistence
├── 🧮 calculations.py         # Attendance calculations, date math
├── ⚙️ setup_tab.py            # Configuration interface
├── 📋 timetable_tab.py        # Weekly schedule display
├── 📅 attendance_calendar.py  # Monthly calendar interface
├── 📈 summary_tab.py          # Statistics dashboard
├── 💾 data.json               # User data (auto-generated)
├── 📝 timetable.md            # Timetable reference
├── 📖 README.md               # This file
└── .gitignore                 # Git ignore rules
```

**Total Code Size**: ~63 KB across 7 Python files

## 🎨 Color Scheme & Visual Language

| Element | Color | Hex Code | Usage |
|---------|-------|----------|-------|
| 🟢 Safe Status | Green | `#28a745` | Attendance ≥75% |
| 🔴 At Risk | Red | `#dc3545` | Attendance <75% |
| 🔵 Theory Classes | Blue | `#007bff` | DAA, TOC, CN, DM |
| 🟣 Lab Classes | Purple | `#7B1FA2` | CN Lab, DAA Lab, Software Lab |
| 🟠 Special Classes | Orange | `#E65100` | Minor, MDM, OE, Honors |
| 🟡 Holidays | Yellow | `#FFF9C4` | Marked holiday dates |
| ⚪ Future/Weekend | Gray | `#F5F5F5` | Upcoming/non-working days |

## 🧮 Attendance Formula

```python
# Present by default model
attended = total_classes - len(absent_dates_until_today)
attendance_percentage = (attended / total) * 100

# Safe classes to skip
safe_to_skip = floor((attended - 0.75 * (total + skips)) / 0.25)
```

## 💾 Data Storage

All data is stored locally in `data.json`:
```json
{
  "batch": "B1/B3",
  "semester_start": "2025-08-01",
  "semester_end": "2025-12-15",
  "holidays": [
    {"start": "2025-10-20", "end": "2025-10-27", "name": "Diwali Break"}
  ],
  "subjects": [
    {
      "name": "DAA",
      "weekly_count": 3,
      "total_override": null,
      "absent_dates": ["2025-11-15", "2025-11-22"]
    }
  ]
}
```

## 🔧 Customization

### Modifying the Timetable
Edit the `TIMETABLE_DATA` dictionary in `data_manager.py`:
```python
TIMETABLE_DATA = {
    "MONDAY": {
        "09:00-10:00": "Subject Name",
        "10:00-11:00": "24CS01TH0302-Subject (Room)",
        # ... more slots
    },
    # ... more days
}
```

### Changing the Window Size
Edit `app.py`:
```python
self.root.geometry("1400x900")  # Width x Height
```

## 🐛 Troubleshooting

### Issue: Calendar not displaying
**Solution**: Install tkcalendar
```bash
pip install tkcalendar
```

### Issue: Data not saving
**Solution**: Check file permissions in the application directory

### Issue: Wrong lab classes showing
**Solution**: Verify batch selection in Setup tab (B1/B3 vs B2/B4)

## �️ Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Language** | Python 3.8+ | Core programming language |
| **GUI Framework** | Tkinter/ttk | Desktop interface |
| **Date Widgets** | tkcalendar | Calendar components |
| **Data Storage** | JSON | Local data persistence |
| **Date/Time** | datetime, calendar | Date calculations |
| **Design Pattern** | Modular MVC-like | Clean architecture |

### Why This Stack?
- ✅ **Lightweight**: < 100 KB total size
- ✅ **Fast**: Native GUI performance
- ✅ **Cross-platform**: Works on Windows, Mac, Linux
- ✅ **Offline**: No internet required
- ✅ **Simple**: Minimal dependencies
- ✅ **Maintainable**: Clean, readable code

## 📝 Development

### Code Architecture
```
┌─────────────────┐
│   app.py        │  ← Entry point, window setup
│  (Main Window)  │
└────────┬────────┘
         │
    ┌────┴─────────────────────────┐
    │                               │
┌───▼────┐                   ┌─────▼────┐
│  UI    │                   │  Core    │
│ Tabs   │◄──────────────────┤ Modules  │
└────────┘                   └──────────┘
│                               │
├─ setup_tab.py               ├─ data_manager.py
├─ timetable_tab.py           ├─ calculations.py
├─ attendance_calendar.py     └─ data.json
└─ summary_tab.py
```

### Key Design Principles
- **Present by Default**: Only track absences (saves time!)
- **Real-time Updates**: Instant recalculation on changes
- **Atomic Operations**: Auto-save after each action
- **Batch-Aware**: Different labs for B1/B3 vs B2/B4
- **User Confirmation**: Dialogs for critical actions
- **Clean Code**: Proper spacing, comments, docstrings

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🌟 Key Highlights

<table>
<tr>
<td width="50%">

### 💪 Powerful Features
- 📊 **Real-time Calculations**
- 🎯 **75% Threshold Tracker**
- 📅 **Google Calendar UI**
- 🖱️ **Right-click Quick Mark**
- 🔄 **One-click Reset**

</td>
<td width="50%">

### 🚀 User Benefits
- ⏱️ **Saves Time**: Mark absences only
- 🎓 **Stay on Track**: Visual warnings
- 📈 **Plan Ahead**: Safe skip calculator
- 💾 **Secure**: Local data storage
- 🖥️ **Offline**: No internet needed

</td>
</tr>
</table>

## 👨‍💻 Author

**Siddhesh**
- 🎓 Software Lab Project - 3rd Semester
- 💻 Python Developer | Student
- 📧 [Your Email]
- 🔗 [LinkedIn](https://linkedin.com/in/yourprofile)

## 🙏 Acknowledgments

- 🐍 Built with **Python** and **Tkinter**
- 📅 Uses **tkcalendar** for date selection widgets
- 💡 Inspired by **Google Calendar's** interface design
- 🎨 Color scheme based on Bootstrap colors
- 👥 Thanks to all contributors and testers

## ⭐ Show Your Support

If you find this project helpful, please consider:
- ⭐ **Star this repository**
- 🐛 Report bugs or suggest features
- 🔧 Contribute improvements
- 📢 Share with your classmates

## 📞 Support

For issues or questions:
1. Check the Troubleshooting section
2. Review the User Guide
3. Check existing issues on GitHub

---

**Note**: This application is designed for educational purposes to help students track their attendance effectively. Always verify your actual attendance with your institution's official records.
