# LingoLink

## Description
**LingoLink** is a voice translation assistant that leverages Watsonx and IBM Watson Speech Libraries to provide real-time translations in multiple languages. The assistant captures voice input, converts it to text, sends the text to Watsonx's flan-ul2 model for translation, and then converts the translated text back to speech. This project integrates natural language processing, speech recognition, and web development to create a comprehensive AI-driven solution for seamless communication across languages. You can watch a short video of the build here: [Lingo Link](https://youtu.be/BZ3pPQsSNFc)

## Features
- **Real-Time Translation**: Provides instantaneous translations in multiple languages using Watsonx's flan-ul2 model.
- **Speech Recognition**: Converts voice input to text using IBM Watson's Speech-to-Text API.
- **Text-to-Speech Conversion**: Translates text back into speech for user interaction.
- **Web-Based Interface**: A user-friendly front-end built with HTML, CSS, JavaScript, Bootstrap, Font Awesome, and JQuery.
- **Flask Back-End**: Manages server-side operations and API requests.
- **Docker Integration**: Ensures consistent application behavior by managing containers with Docker.

## Installation

### Prerequisites
- Docker installed on your machine
- IBM Watson API keys for Speech-to-Text and Text-to-Speech services
- Watsonx API key for translation services

### Steps
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/LingoLink.git
   cd LingoLink

2. **Set Up Environment Variables:**
    
    Create a .env file in the project root directory and add your IBM Watson and Watsonx API keys:

        WATSON_API_KEY=your_ibm_watson_api_key_here
        WATSONX_API_KEY=your_watsonx_api_key_here

3. **Build the Docker Image:**

    Use Docker to build the application image:

        docker build -t lingolink-app .

4. **Run the Docker Container:**

    Start the application by running the Docker container:

        docker run -p 5000:5000 lingolink-app

5. **Access the Application:**

    Open your web browser and navigate to http://localhost:5000 to interact with the LingoLink voice translation assistant.


## Usage

1. **Voice Input:** Speak into your microphone, and the assistant will capture your voice.
2. **Translation:** The captured speech is converted to text and sent to Watsonx's flan-ul2 model for translation.
3. **Output:** The translated text is then converted back to speech, providing you with the translation in the target language.


## Example Code

Here's a snippet from the Flask API that handles the speech-to-text and text-to-speech processes:

    from flask import Flask, request, jsonify
    import watson_developer_cloud as watson

    app = Flask(__name__)

    @app.route('/translate', methods=['POST'])
    def translate():
        data = request.json
        text = data['text']
        
        # Translate text using Watsonx
        translated_text = watsonx_translate(text)
        
        # Convert translated text to speech
        speech = watson.TextToSpeechV1().synthesize(
            translated_text, accept='audio/wav', voice="en-US_AllisonV3Voice"
        ).get_result().content
        
        return jsonify({'speech': speech.decode('ISO-8859-1')})

    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=5000)

## Deployment

The application is designed to be deployed using Docker, ensuring consistent performance across different environments. Rebuild the Docker image and run the container to deploy the application.

## License
This project is licensed under the MIT License. See the LICENSE file for more information.
