### **What the app does:**

This app is a chatbot that integrates with Google Maps and Google Places APIs to help users find the nearest location of a specified type, provide details about the location, and allow users to rate their experience. Here's a breakdown of its functionality:

---

### **Core Features:**

1. **User Interaction:**
   - The app is a Telegram bot that interacts with users via chat.
   - Users can initiate a conversation with `/start` and stop it with `/stop`.
   - The bot prompts users step-by-step to:
     - Specify a type of location they want to find (e.g., restaurant, gas station).
     - Share their current location.
     - Indicate the maximum distance they are willing to travel.

2. **Finding the Nearest Location:**
   - The app uses Google Maps and Google Places APIs to:
     - Geocode the user's current location.
     - Perform a nearby search based on the user’s specified location type and radius.
     - Calculate the distances between the user’s location and potential destinations.
   - The app adjusts distances based on previously stored user ratings for the locations to prioritize higher-rated places.

3. **Details and Recommendations:**
   - The app recommends the best-matched location based on adjusted distance and ratings.
   - It provides detailed information about the recommended location, including:
     - Name
     - Address
     - Phone number
     - Google rating

4. **User Ratings:**
   - After the user visits the recommended location, the bot asks for a rating (1-5).
   - Ratings are stored locally in a file (`StoredRatings.txt`) for future use.
   - The app updates the stored ratings and uses them to refine future recommendations.

5. **Persistence and Local Storage:**
   - User ratings and associated data are stored in `StoredRatings.txt` as a JSON object.
   - The stored data is used to adjust the ranking of locations in future queries.

---

### **Key Components:**

1. **`MessageCounter` Class (Telegram Bot Logic):**
   - Handles the conversation flow with users.
   - Maintains the bot's state (e.g., waiting for location type, radius, or rating).
   - Interacts with the `get_nearest_location` function to fetch and provide location recommendations.

2. **`get_nearest_location` Function:**
   - Conducts a search for nearby places using the Google Places API.
   - Adjusts distances of locations based on user ratings stored in `StoredRatings.txt`.
   - Identifies and returns the best-matched location.

3. **Google Maps and Places Integration:**
   - Geocoding user-provided addresses to coordinates.
   - Using `distance_matrix` to calculate distances between the user's location and potential destinations.
   - Querying for places of a specific type using `nearby_search`.

4. **Local Rating System:**
   - Allows users to provide feedback on their experience with recommended locations.
   - Stores these ratings for use in prioritizing highly-rated locations in future queries.

---

### **Use Case:**
The app can be used as a personalized location recommendation tool for Telegram users. Examples include:
- Finding the best nearby restaurant based on user ratings.
- Locating essential services (e.g., gas stations, pharmacies) within a specified distance.
- Building a system that learns from user feedback to improve recommendations over time.
