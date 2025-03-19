
# React Quiz App Explanation

## **Overview**  
This is a **React-based Quiz App** that fetches quiz questions from an API, manages state using `useReducer`, and dynamically updates the UI based on user interactions. It consists of multiple components handling different functionalities.

---

## **Main File: `App.js`**  
### **1. Importing Components and Hooks**  
The `App.js` file imports various components (`Main`, `Header`, `Loader`, etc.) and React hooks (`useEffect`, `useReducer`).

### **2. Defining Constants and Initial State**  
- `SECS_PER_QUESTION = 30;` → Each question has 30 seconds.  
- `initialState` → Holds the quiz state with properties like `questions`, `status`, `index`, `points`, `highscore`, etc.  

### **3. Reducer Function for State Management**  
The `reducer` function updates the state based on actions:
- `dataReceived` → Stores fetched questions and updates `status` to "ready".  
- `dataFailed` → Sets status to "error" if data fetching fails.  
- `start` → Begins the quiz and initializes the timer.  
- `newAnswer` → Checks if the selected answer is correct and updates the score.  
- `nextQuestion` → Moves to the next question.  
- `finish` → Ends the quiz and updates the high score.  
- `restart` → Resets the quiz.  
- `tick` → Decreases the remaining time per second.

### **4. Using `useReducer` for State Management**  
The `useReducer` hook initializes the state and dispatches actions to update it.

### **5. Fetching Quiz Data (`useEffect`)**  
- Fetches quiz questions from `"http://localhost:8000/questions"` on component mount.
- Stores data in `questions` using `dispatch({ type: "dataReceived", payload: data })`.

### **6. Rendering the UI Based on Quiz Status**  
- **"loading"** → Shows `<Loader />`.  
- **"error"** → Shows `<Error />`.  
- **"ready"** → Displays `<StartScreen />`.  
- **"active"** → Shows quiz questions, progress, timer, and navigation buttons.  
- **"finished"** → Displays `<FinishedScreen />` with results.  

---

## **Component Breakdown**  

### **1. `FinishedScreen.js`**  
- Displays quiz results and percentage score.  
- Shows an emoji based on performance.  
- Includes a "Restart Quiz" button that resets the quiz state.

### **2. `NextButton.js`**  
- Displays the "Next" button when an answer is selected.  
- Moves to the next question or finishes the quiz if it's the last question.

### **3. `Options.js`**  
- Displays multiple-choice answer buttons.  
- Disables options after selecting an answer.  
- Highlights the correct answer in green and incorrect ones in red.

### **4. `Progress.js`**  
- Displays a progress bar indicating the current question number.  
- Shows total points and maximum possible points.

### **5. `Question.js`**  
- Displays the current quiz question.  
- Uses the `<Options />` component to show answer choices.

### **6. `StartScreen.js`**  
- Displays a welcome message.  
- Shows the total number of questions.  
- Has a "Let's Start" button that starts the quiz.

### **7. `Timer.js`**  
- Counts down the remaining time.  
- Uses `setInterval` inside `useEffect` to update time every second.  
- Dispatches the `"tick"` action to decrease the time.  
- Clears the timer when the component unmounts.

---

## **How the Quiz App Works**  
1. **Loads Data**:  
   - Fetches questions from an API.  
   - Displays a loading screen until the data is received.  
2. **Starting the Quiz**:  
   - User clicks "Let's Start", and the quiz begins.  
   - A timer starts counting down.  
3. **Answering Questions**:  
   - User selects an option.  
   - If correct, points are added.  
   - Moves to the next question.  
4. **Quiz Completion**:  
   - At the last question, clicking "Next" finishes the quiz.  
   - Displays total score and high score.  
   - Option to restart the quiz.
