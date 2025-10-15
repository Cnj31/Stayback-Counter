import streamlit as st
from datetime import datetime
import base64

# ---- Background Image Function ----
def add_bg_from_local(image_file):
    with open(image_file, "rb") as image:
        encoded_string = base64.b64encode(image.read())
    st.markdown(
        f"""
        <style>
        .stApp {{
            background-image: url("data:image/jpg;base64,{encoded_string.decode()}");
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
        }}
        /* Transparent overlay for readability */
        .main {{
            background-color: rgba(255, 255, 255, 0.75);
            border-radius: 12px;
            padding: 20px;
        }}
        /* Headings */
        h1 {{
            color: #1B262C;
            text-align: center;
            font-family: 'Poppins', sans-serif;
        }}
        h2, h3 {{
            color: #0078D7;
        }}
        /* General text */
        p, span, div {{
            color: #3C4858;
            font-family: 'Poppins', sans-serif;
        }}
        /* Info and highlight boxes */
        .stAlert {{
            background: linear-gradient(90deg, #0078D7, #00B4D8);
            color: white !important;
            border-radius: 10px;
        }}
        /* Footer motivational text */
        .footer {{
            text-align: center;
            font-style: italic;
            color: #6C63FF;
            margin-top: 20px;
        }}
        </style>
        """,
        unsafe_allow_html=True
    )

# ---- Background Music Function ----
def play_fadein_audio(file_path):
    with open(file_path, "rb") as audio_file:
        audio_bytes = audio_file.read()
        base64_audio = base64.b64encode(audio_bytes).decode()

        audio_html = f"""
        <audio id="bg-audio" loop>
            <source src="data:audio/mp3;base64,{base64_audio}" type="audio/mp3">
        </audio>

        <script>
        const audio = document.getElementById('bg-audio');
        let hasPlayed = false;

        function startAudio() {{
            if (!hasPlayed) {{
                audio.volume = 0;
                audio.play();
                hasPlayed = true;
                let fadeIn = setInterval(() => {{
                    if (audio.volume < 0.6) {{
                        audio.volume = Math.min(0.6, audio.volume + 0.02);
                    }} else {{
                        clearInterval(fadeIn);
                    }}
                }}, 200);
            }}
        }}

        // Trigger fade-in sound on any click or scroll
        window.addEventListener('click', startAudio);
        window.addEventListener('scroll', startAudio);
        </script>
        """
        st.markdown(audio_html, unsafe_allow_html=True)



# ---- Call background and sound ----
add_bg_from_local("pexels.jpg")
play_fadein_audio("ocean-waves-266187.mp3")

# ---- Page Config ----
st.set_page_config(page_title="My Ireland Stay-Back Countdown 🇮🇪", page_icon="⏳", layout="centered")

# ---- Header ----
st.title("My Ireland Stay-Back Countdown")
st.write("Track how many days are left in your 2-year stay-back journey in Ireland.")

# ---- Date Setup ----
start_date = datetime(2025, 10, 28)  # Graduation date
end_date = datetime(2027, 10, 28)    # 2 years later
now = datetime.now()

# ---- Calculate Remaining Time ----
remaining = end_date - now
days = remaining.days
hours, remainder = divmod(remaining.seconds, 3600)
minutes, seconds = divmod(remainder, 60)

# ---- Progress Bar ----
total_duration = (end_date - start_date).days
progress = max(0.0, min(1.0, (total_duration - days) / total_duration))
st.progress(progress)

# ---- Countdown Display ----
st.metric(label="Days Remaining", value=f"{days} days")
st.write(f"🕒 **{days} days, {hours} hours, {minutes} minutes, {seconds} seconds** left.")

# ---- Info Box ----
st.info("Every day counts — make it meaningful 💪")

# ---- Motivational Quotes ----
quotes = [
    "Keep learning, keep growing 🌱",
    "Each day is a step toward your dream 🇮🇪",
    "You’re building your story — one day at a time 🚀"
]
st.markdown(f"<div class='footer'>💬 *{quotes[days % len(quotes)]}*</div>", unsafe_allow_html=True)
