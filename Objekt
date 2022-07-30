import numpy as np
import cv2
from PIL import ImageGrab
from PIL.Image import NONE

class Object:
    def __init__(self, path):
        bild = cv2.imread(path, 0)
        self.bild = bild
        self.width = bild.shape[1]
        self.height = bild.shape[0]
        self.position = NONE

    def match(self,scr) :
        '''
        Position des Dinos ermitteln
        '''
        res = cv2.matchTemplate(scr, self.bild, cv2.TM_CCOEFF_NORMED)
        minVal, maxVal, miniLoc, maxLoc = cv2.minMaxLoc(res)
        startloc = maxLoc
        endloc = (startloc[0] + self.width, startloc[1] + self.height)
        if maxVal > 0.8:
            self.position = (startloc, endloc)
            return True
        else:
            self.position = None
            return False


def grab_Screen(bbox=None):
    bild = ImageGrab.grab(bbox=bbox)  # macht ein Screenshot
    bild = np.array(bild)
    bild = cv2.cvtColor(bild, cv2.COLOR_RGB2BGR)  # Farbcode: RGB zu BGR
    return bild
