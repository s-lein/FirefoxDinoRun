if __name__ == '__main__':
    import cv2
    from Objekt import Object, grab_Screen
    import  pyautogui as pag
    import time
    StartTime =time.time()
    prevTime =time.time()
    speedrate = 1.5
    #Anfangs Sprungdistanz zum Objekt
    tresholdDistance = 130

    player=[Object('SpielObjekte/Dino.png')]
    enemys=[Object('SpielObjekte/Kaktus1.png'),Object('SpielObjekte/Kaktus2.png'),Object('SpielObjekte/Vogel.png')]

    while 1:
        bild = grab_Screen()
        bild = cv2.cvtColor(bild, cv2.COLOR_BGR2GRAY)
        if player[0].match(bild):
            '''
            Die Größe des Macthing-Bildschirmes verringern umd 
            die "Tastrate" und folglich die Performance erhöhen
            '''
            topleft_x = int(player[0].position[0][0] - player[0].width)
            topleft_y = int(player[0].position[0][1] - 0.75*player[0].height)
            bottomRight_x = int(player[0].position[1][0] + 7*player[0].width)
            bottomRight_y = int(player[0].position[1][1] + player[0].height)
            screenStart = (topleft_x, topleft_y)
            screenEnd = (bottomRight_x, bottomRight_y)
            break

    pag.press('space')

    while 1:
        bild_o = grab_Screen(bbox=(*screenStart, *screenEnd))
        bild = cv2.cvtColor(bild_o, cv2.COLOR_BGR2GRAY)

    # Sprug Zeitpunkt verändern
        if time.time()-prevTime > 1:
            if time.time() - StartTime < 150:
                tresholdDistance += speedrate
                prevTime = time.time()
    # Rechteck um den Dino machen
        if player[0].match(bild):
            cv2.rectangle(bild_o, player[0].position[0], player[0].position[1], (255,0,0), 2) 
    # Rechteck um Gegner machen
        for enemy in enemys:
            if enemy.match(bild):
                cv2.rectangle(bild_o, enemy.position[0], enemy.position[1], (0,0,255), 2)

                if player[0].position:

                    horizontalDistance = enemy.position[0][0] - player[0].position[1][0]
                    verticalDistance = player[0].position[0][1] - enemy.position[1][1]

                    if horizontalDistance < tresholdDistance and verticalDistance < 3:
                        pag.press('space')
                        break


        cv2.imshow("Screen", bild_o)

        if cv2.waitKey(1) == ord('q'):
            break
