Food Health Detector 🥗

A web application that analyzes food items to determine if they're organic or inorganic, and provides AI-powered health recommendations based on age groups.

Features
Food Analysis: Classifies food items as organic or inorganic/junk food

Age-Specific Recommendations: Provides tailored health advice for children, teenagers, adults, and elders

Nutritional Charts: Visual representation of food nutritional value using Chart.js

AI-Powered Suggestions: Utilizes OpenAI API for personalized recommendations

Data Storage: Saves analysis results to Supabase realtime database

User-Friendly Interface: Clean, responsive design with quick-select food options

Technology Stack
Frontend
HTML5, CSS3, JavaScript (ES6+)

Chart.js for data visualization

Responsive design with Flexbox and CSS Grid

Backend
Python Flask web framework

MySQL database integration

OpenAI API integration for recommendations

Supabase for realtime database

Security
SQL injection prevention

Input validation and sanitization

Installation & Setup
Prerequisites
Python 3.8+

Node.js (for optional frontend tooling)

Supabase account

OpenAI API account

Backend Setup
Clone the repository:

bash
git clone <repository-url>
cd food-health-detector
Create a virtual environment and install dependencies:

bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install flask flask-cors openai supabase python-dotenv
Set up environment variables:

bash
cp .env.example .env
Edit .env with your credentials:

text
OPENAI_API_KEY=your_openai_api_key_here
SUPABASE_URL=your_supabase_url_here
SUPABASE_KEY=your_supabase_key_here
FLASK_ENV=development
Initialize the database:

sql
CREATE DATABASE food_health;
USE food_health;

CREATE TABLE food_analyses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    food_name VARCHAR(255) NOT NULL,
    is_organic BOOLEAN NOT NULL,
    age_group ENUM('child', 'teenage', 'adult', 'elder') NOT NULL,
    recommendations JSON,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Run the Flask application:

bash
python app.py
Frontend Setup
The frontend is contained in a single HTML file that can be directly opened in a browser, or served via the Flask backend.

For development with live reload, you can use a simple HTTP server:

bash
# Using Python
python -m http.server 8000

# Using Node.js http-server
npx http-server
API Endpoints
POST /analyze
Analyzes a food item and returns recommendations.

Request Body:

json
{
  "food": "apple",
  "age_group": "child"
}
Response:

json
{
  "food": "apple",
  "is_organic": true,
  "recommendations": [
    "Apples are excellent for children...",
    "Include apples in daily snacks...",
    "Try different apple varieties..."
  ]
}
GET /history
Retrieves analysis history for a user (requires authentication).

POST /register
Registers a new user account.

POST /login
Authenticates a user and returns a session token.

Project Structure
text
food-health-detector/
├── app.py                 # Flask application
├── index.html            # Main frontend file
├── requirements.txt      # Python dependencies
├── .env                  # Environment variables (gitignored)
├── README.md            # This file
└── database/
    └── schema.sql       # Database schema
Usage
Open the application in your web browser

Enter a food item or select from the quick options

Choose an age group from the dropdown

Click "Analyze Food" to get results

View the nutritional chart and AI recommendations

Security Features
Prepared statements for all database queries to prevent SQL injection

Input validation on both client and server side

Environment variables for sensitive credentials

CORS configuration for API endpoints

Supabase Integration
The application uses Supabase for realtime database functionality:

Create a Supabase account and project at https://supabase.com

Create a table called food_analyses with appropriate columns

Add your Supabase URL and key to the environment variables

OpenAI Integration
The application uses OpenAI's API to generate food recommendations:

Sign up for an OpenAI API key at https://platform.openai.com

Add your API key to the environment variables

The application will use the API to generate age-specific recommendations

Customization
You can extend the application by:

Adding more food items to the organic/inorganic lists

Customizing the recommendation prompts for OpenAI

Adding more age groups or dietary preferences

Implementing user profiles and history

Adding more detailed nutritional information

Contributing
Fork the repository

Create a feature branch

Make your changes

Add tests if applicable

Submit a pull request

License
This project is licensed under the MIT License - see the LICENSE file for details.

Troubleshooting
Common Issues
ModuleNotFoundError: Ensure all Python dependencies are installed

API errors: Check your OpenAI and Supabase credentials

Database connection issues: Verify your MySQL server is running

CORS errors: Ensure the Flask-CORS extension is properly configured

Getting Help
If you encounter issues not covered here, please open an issue on the GitHub repository with details about the problem.

Future Enhancements
Image recognition for food items

Meal planning functionality

Integration with nutrition databases

Mobile app version

Social features for sharing healthy recipes

Personalized dietary tracking