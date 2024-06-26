<script>
    // Generate a random number between 1 and 100 when the component is initialized
    const randomNumber = Math.floor(Math.random() * 100) + 1;
    // Initialize variables to store user input, messages, and button/input states
    let userGuess = '';
    let message = '';
    let messageColor = '';
    let submitButtonState = false; // Track Submit Button state
    let inputState = false; // Track Input Box state
    let submitButtonBackgroundColor = ''; // Variable to change the default CSS color of the submit button
    
    // Function to handle the submission of the user's guess
    function submitGuess() {
      const guess = parseInt(userGuess);
  
      // Check if the user's input is valid
      if (isNaN(guess) || guess < 1 || guess > 100) {
        // Display an error message if the input is not a valid number
        message = "Please enter a valid number between 1 and 100.";
      } else {
        // Compare the user's guess with the random number
        if (guess === randomNumber) {
          // If the guess is correct, display a success message
          message = "Congratulations! You guessed the correct number! Refresh the page to start again.";
          messageColor = "green";
          submitButtonState = true; // Disable the submit button
          inputState = true; // Disable the input box
          submitButtonBackgroundColor = 'gray'; // Change the background color of the submit button
        } else if (guess < randomNumber) {
          // If the guess is too low, provide a hint to guess higher
          message = "Try again! Your guess is too low.";
          messageColor = "blue";
        } else {
          // If the guess is too high, provide a hint to guess lower
          message = "Try again! Your guess is too high.";
          messageColor = "red";
        }
      }
    }
</script>

<style>
    /* Include the styles from the external CSS file */
    @import 'styles.css';
    @import 'main.css';
</style>

<main>
    <!-- Main content of the component -->
    <h1>Guess the Number Game</h1>
    <p>Guess a number between 1 and 100:</p>
    <!-- Input box for user's guess, disabled based on inputState, and bound to userGuess -->
    <input type="number" disabled={inputState} bind:value={userGuess} />
    <!-- Submit button, with click event handler and disabled attribute based on submitButtonState -->
    <button on:click={submitGuess} disabled={submitButtonState} style="background-color: {submitButtonBackgroundColor}">Submit Guess</button>
    <!-- Display the message with color based on messageColor -->
    <p style="color: {messageColor}">{message}</p>
</main>
