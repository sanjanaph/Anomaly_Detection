
# Anomaly_Detection

# 🔍 Healthcare Audit Log Anomaly Detection System

A comprehensive machine learning-based anomaly detection system designed to identify suspicious activities in healthcare laboratory information system (LIS) audit logs using Isolation Forest algorithm.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Data Structure](#data-structure)
- [Anomaly Detection Methods](#anomaly-detection-methods)
- [Feature Engineering](#feature-engineering)
- [Visualization](#visualization)
- [Results Interpretation](#results-interpretation)
- [Configuration](#configuration)
- [File Structure](#file-structure)
- [Dependencies](#dependencies)
- [Usage Examples](#usage-examples)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This system analyzes healthcare audit logs to detect anomalous user behaviors that could indicate:
- **Security breaches** (unauthorized access)
- **Insider threats** (malicious employee actions)
- **System misuse** (policy violations)
- **Account compromise** (stolen credentials)
- **Unusual operational patterns** (workflow deviations)

The system uses **Isolation Forest**, an unsupervised machine learning algorithm that excels at detecting outliers in high-dimensional data without requiring labeled training data.

## ✨ Features

### 🔧 Core Functionality
- **Unsupervised Anomaly Detection** using Isolation Forest
- **Multi-dimensional Feature Analysis** across temporal, behavioral, and geographic patterns
- **Real-time Risk Scoring** with interpretable anomaly scores
- **Comprehensive Visualization** with interactive charts and graphs
- **Detailed Reporting** with actionable insights

### 🎛️ Detection Capabilities
- **Temporal Anomalies**: Unusual timing patterns (off-hours, weekends)
- **Behavioral Anomalies**: Deviant user action patterns
- **Geographic Anomalies**: Suspicious location-based activities
- **Role-based Anomalies**: Actions inconsistent with user roles
- **Organizational Anomalies**: Unusual patterns within organizations

### 📊 Analytics & Reporting
- Anomaly rate by role, action type, and time
- Feature importance analysis
- Top anomalous users identification
- Geographic distribution of anomalies
- Organization-level anomaly patterns

## 🚀 Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Required Packages
```bash
pip install numpy==1.24.3
pip install pandas==2.1.4
pip install matplotlib==3.8.2
pip install scikit-learn==1.3.2
pip install openpyxl
pip install geopy
pip install faker
pip install seaborn
```

### Quick Installation
```bash
# Clone or download the project
cd anomaly_detection

# Install all dependencies
pip install -r requirements.txt  # (if available)
# OR install individually as shown above
```

## ⚡ Quick Start

1. **Prepare Your Data**
   - Place your audit log Excel file in the project directory
   - Update the `DATA_PATH` variable in the notebook to point to your file

2. **Run the Analysis**
   ```python
   # Open and run the Jupyter notebook
   jupyter notebook rules_generation.ipynb
   ```

3. **View Results**
   - Anomaly detection results will be displayed in the notebook
   - Visualizations will show patterns and distributions
   - Detailed analysis will identify the most suspicious activities

## 📊 Data Structure

### Input Data Format
The system expects an Excel file with the following columns:

| Column | Type | Description |
|--------|------|-------------|
| `userid` | Integer | Unique user identifier |
| `formatteddisplayname` | String | User's display name |
| `email` | String | User's email address |
| `rolename` | String | User's role (Admin, Lab Technician, etc.) |
| `actionperformed` | String | Action taken by the user |
| `auditdate` | DateTime | Timestamp of the action |
| `city` | String | City where action was performed |
| `organizationname` | String | Organization name |
| `user region` | String | Geographic region |
| `lat` | Float | Latitude coordinate (optional) |
| `lng` | Float | Longitude coordinate (optional) |

### Sample Data
```python
# Example record
{
    'userid': 1001,
    'formatteddisplayname': 'John Doe',
    'rolename': 'Lab Technician',
    'actionperformed': 'Viewed Case Information',
    'auditdate': '2024-01-15 14:30:00',
    'city': 'Boston',
    'organizationname': 'Health Lab Solutions'
}
```

## 🔍 Anomaly Detection Methods

### Isolation Forest Algorithm
- **Type**: Unsupervised ensemble method
- **Principle**: Isolates anomalies by randomly selecting features and splitting values
- **Advantages**: 
  - No labeled training data required
  - Handles high-dimensional data well
  - Robust to outliers in training data
  - Fast training and prediction

### Feature Engineering Pipeline
1. **Temporal Features**
   - Hour of day
   - Day of week
   - Weekend indicator
   - After-hours indicator

2. **Behavioral Features**
   - User action frequency
   - Unique actions per user
   - Geographic diversity

3. **Categorical Encoding**
   - Role encoding
   - Action encoding
   - Organization features

4. **Geographic Features**
   - Coordinate availability
   - Location diversity metrics

## 📈 Visualization

The system provides four key visualizations:

### 1. Anomaly Score Distribution
- Histogram showing the distribution of anomaly scores
- Red line indicates the anomaly threshold
- Helps understand the overall anomaly landscape

### 2. Anomalies by Hour of Day
- Bar chart showing anomaly rates across different hours
- Identifies peak anomaly hours
- Useful for temporal pattern analysis

### 3. Anomalies by Role
- Bar chart comparing anomaly rates across user roles
- Identifies which roles show more suspicious behavior
- Helps in role-based security analysis

### 4. User Behavior Scatter Plot
- Scatter plot of user action frequency vs anomaly score
- Color-coded by anomaly status
- Identifies behavioral outliers

## 📋 Results Interpretation

### Anomaly Scores
- **Range**: -1 to +1
- **Interpretation**:
  - **Lower scores** = More anomalous
  - **Higher scores** = More normal
  - **Threshold**: Automatically determined by contamination parameter

### Key Metrics
- **Anomaly Rate**: Percentage of records flagged as anomalous
- **Feature Importance**: Which features contribute most to anomaly detection
- **Top Anomalous Users**: Users with highest anomaly scores
- **Pattern Analysis**: Breakdown by role, time, location, and organization

### Actionable Insights
1. **Immediate Investigation**: Focus on highest-scoring anomalies
2. **Pattern Analysis**: Look for systematic issues in specific roles/times
3. **Geographic Clustering**: Investigate location-based anomalies
4. **Temporal Trends**: Monitor time-based anomaly patterns

## ⚙️ Configuration

### Isolation Forest Parameters
```python
iso_forest = IsolationForest(
    contamination=0.1,      # Expected anomaly rate (10%)
    random_state=42,        # For reproducible results
    n_estimators=100        # Number of trees in the forest
)
```

### Feature Selection
```python
isolation_features = [
    'hour_of_day', 'day_of_week', 'is_weekend', 'is_after_hours',
    'user_action_frequency', 'user_unique_actions', 'user_geographic_diversity',
    'role_encoded', 'action_encoded', 'org_size', 'has_coordinates'
]
```

### Customization Options
- **Contamination Rate**: Adjust based on expected anomaly percentage
- **Feature Selection**: Add or remove features based on your data
- **Visualization**: Modify charts and analysis based on your needs

## 📁 File Structure

```
anomaly_detection/
├── README.md                          # This file
├── rules_generation.ipynb            # Main analysis notebook
├── Caseauditdetails_LIS 3.xlsx       # Sample audit log data
├── requirements.txt                   # Python dependencies (optional)
└── uad/                              # Additional utilities (if any)
```

## 📦 Dependencies

### Core Libraries
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **scikit-learn**: Machine learning algorithms
- **matplotlib**: Plotting and visualization
- **seaborn**: Statistical data visualization

### Data Processing
- **openpyxl**: Excel file reading/writing
- **geopy**: Geographic calculations
- **faker**: Synthetic data generation (for testing)

### Version Compatibility
- Python: 3.8+
- pandas: 2.1.4
- scikit-learn: 1.3.2
- numpy: 1.24.3

## 💡 Usage Examples

### Basic Usage
```python
# Load data
df = pd.read_excel("Caseauditdetails_LIS 3.xlsx")

# Run anomaly detection
iso_forest = IsolationForest(contamination=0.1, random_state=42)
iso_forest.fit(X)
anomalies = iso_forest.predict(X)

# Analyze results
anomaly_count = sum(anomalies == -1)
print(f"Detected {anomaly_count} anomalies")
```

### Custom Feature Engineering
```python
# Add custom features
df['custom_metric'] = df['user_action_frequency'] / df['org_size']

# Include in isolation forest
features = ['hour_of_day', 'custom_metric', 'role_encoded']
X = df[features]
```

### Threshold Tuning
```python
# Adjust contamination based on your data
contamination_rates = [0.05, 0.1, 0.15, 0.2]
for rate in contamination_rates:
    iso_forest = IsolationForest(contamination=rate)
    iso_forest.fit(X)
    anomalies = iso_forest.predict(X)
    print(f"Rate {rate}: {sum(anomalies == -1)} anomalies")
```

## 🔧 Troubleshooting

### Common Issues

#### 1. Import Errors
```bash
# Error: ModuleNotFoundError
pip install <missing_package>

# Error: Version conflicts
pip install --upgrade <package_name>
```

#### 2. Data Loading Issues
```python
# Error: Excel file not found
# Solution: Check file path and permissions
DATA_PATH = r"C:\path\to\your\file.xlsx"

# Error: Column not found
# Solution: Check column names in your data
print(df.columns.tolist())
```

#### 3. Memory Issues
```python
# For large datasets, consider sampling
df_sample = df.sample(n=10000, random_state=42)
X = df_sample[features]
```

#### 4. Visualization Issues
```python
# Error: Matplotlib backend issues
import matplotlib
matplotlib.use('TkAgg')  # or 'Agg' for headless
```

### Performance Optimization
- **Large Datasets**: Use data sampling or chunking
- **Memory Usage**: Monitor RAM usage with large feature sets
- **Processing Time**: Adjust `n_estimators` for faster training

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/new-feature`
3. **Make your changes** and test thoroughly
4. **Submit a pull request** with a clear description

### Development Guidelines
- Follow PEP 8 style guidelines
- Add docstrings to new functions
- Include unit tests for new features
- Update documentation for significant changes

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support

For questions, issues, or contributions:
- **Create an issue** in the repository
- **Check the troubleshooting section** above
- **Review the documentation** for common solutions

## 🔮 Future Enhancements

- **Real-time Detection**: Stream processing capabilities
- **Additional Algorithms**: LOF, One-Class SVM integration
- **Dashboard Interface**: Web-based visualization
- **Alert System**: Automated notification system
- **Model Persistence**: Save/load trained models
- **A/B Testing**: Compare different anomaly detection approaches

---

**Built with ❤️ for Healthcare Security**

*This system helps protect sensitive healthcare data by identifying potential security threats and policy violations in audit logs.*

