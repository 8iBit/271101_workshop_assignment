# 271101_workshop_assignment

# import library
import cv2
import mediapipe as mp

# กำหนดตัวแปร และค่าเริ่มต้นของตัวแปร
Hand = "None"
Fing1 = "Thumb : Off"
Fing2 = "Index  : Off"
Fing3 = "Middle : Off"
Fing4 = "Ring   : Off"
Fing5 = "Little  : Off"

# กำหนดตัวแปร cam (ในวงเล็บของ VideoCapture เป็น 0 เพราะเป็นพอร์ตของกล้องที่ติดมากับโน๊ตบุ๊ค ถ้าใช้กล้องเสริม/กล้องภายนอกค่าในวงเล็บก็จะเป็นเลขอื่นที่ไม่ใช่ 0)
cam = cv2.VideoCapture(0)
mpHands = mp.solutions.hands
hands = mpHands.Hands()
mpDraw = mp.solutions.drawing_utils

# loop นี้จะทำงานก็ต่อเมื่อหน้าจอแสดงผล(หน้าจอกล้อง)เปิด กำหนดตัวแปร finger, check, imgG, imgRGB, results
while cam.isOpened():
    finger = []
    check, frame = cam.read()
    imgG = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    imgRGB = cv2.cvtColor(imgG, cv2.COLOR_GRAY2RGB)
    results = hands.process(imgRGB)

# ถ้าเจอมือในจอแสดงภาพ(หน้าจอกล้อง)ให้ทำงาน และกำหนดตัวแปร handLms, id, lm, h, w, c, cx, cy
    if results.multi_hand_landmarks:
        for handLms in results.multi_hand_landmarks:
            for id, lm in enumerate(handLms.landmark):
                h, w, c = frame.shape
                cx, cy = int(lm.x * w), int(lm.y * h)

# เปรียบเทียบ id และกำหนดค่าของตัวแปร id, cx
                if id == 4 :
                    id4 = int(id)
                    cx4 = cx 
                if id == 3 :
                    id3 = int(id)
                    cx3 = cx
                if id == 6 :
                    id6 = int(id)
                    cy6 = cy
                if id == 8 :
                    id8 = int(id)
                    cy8 = cy
                if id == 10:
                    id10 = int(id)
                    cy10 = cy
                if id == 12 :
                    id12 = int(id)
                    cy12 = cy
                if id == 14 :
                    id14 = int(id)
                    cy14 = cy
                if id == 16 :
                    id16 = int(id)
                    cy16 = cy
                if id == 18 :
                    id18 = int(id)
                    cy18 = cy
                if id == 20 :
                    id20 = int(id)
                    cy20 = cy
                if id == 9 :
                    id9 = int(id)
                    cx9 = cx
                if id == 13 :
                    id13 = int(id)
                    cx13 = cx 

# (ตรวจสอบมือว่าเป็นข้างไหน? ซึ่งถ้าตรงเงื่อนไขนี้จะเป็นข้างขวา) ถ้าตรงเงื่อนไข ให้กำหนดค่าของตัวแปร Hand, Fing1 ,Fing2 ,Fing3 ,Fing4 ,Fing5 ใหม่
            if cx9 > cx13:
                Hand = "Right"
                if cx4 > cx3: Fing1 =   "Thumb : On"
                else: Fing1=            "Thumb : Off"
                if cy6 > cy8: Fing2 =   "Index  : On"
                else: Fing2=            "Index  : Off"
                if cy10 > cy12: Fing3 = "Middle : On"
                else: Fing3=            "Middle : Off"
                if cy14 > cy16: Fing4 = "Ring   : On"
                else: Fing4=            "Ring   : Off"
                if cy18 > cy20: Fing5 = "Little  : On"
                else: Fing5=            "Little  : Off"

# ถ้าไม่ตรงเงื่อนไขจาก if ข้างบน ให้กำหนดค่าของตัวแปร Hand, Fing1 ,Fing2 ,Fing3 ,Fing4 ,Fing5 ใหม่
            else:
                Hand = "Left"
                if cx3 > cx4: Fing1 =   "Thumb : On"
                else: Fing1=            "Thumb : Off"
                if cy6 > cy8: Fing2 =   "Index  : On"
                else: Fing2=            "Index  : Off"
                if cy10 > cy12: Fing3 = "Middle : On"
                else: Fing3=            "Middle : Off"
                if cy14 > cy16: Fing4 = "Ring   : On"
                else: Fing4=            "Ring   : Off"
                if cy18 > cy20: Fing5 = "Little  : On"
                else: Fing5=            "Little  : Off"
            mpDraw.draw_landmarks(frame, handLms, mpHands.HAND_CONNECTIONS)

# ถ้าตรงเงื่อนไข ให้แสดงตัวอักษรในจอแสดงภาพ(หน้าจอกล้อง)
            if cx9 > cx13:
                cv2.putText(frame, Hand, (15,25), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing1, (15,45), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing2, (15,65), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing3, (15,85), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing4, (15,105), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing5, (15,125), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)

# ถ้าไม่ตรงเงื่อนไขจาก if ข้างบน ให้แสดงตัวอักษรในจอแสดงภาพ(หน้าจอกล้อง) 
            else :
                cv2.putText(frame, Hand, (525,25), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing1, (525,45), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing2, (525,65), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing3, (525,85), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing4, (525,105), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)
                cv2.putText(frame, Fing5, (525,125), cv2.FONT_HERSHEY_PLAIN, 1, (0,0,100), 2)

# แสดงตัวอักษรในหน้าจอแสดงภาพ(หน้าจอกล้อง)ว่า "Press Z toclose..."
    cv2.putText(frame, "Press Z to close...", (460,460), cv2.FONT_HERSHEY_PLAIN, 1, (100,0,100), 2)

# ถ้าตัวแปร check เป็นจริง (ซึ่งก็เป็นจริงอยู่แล้ว...) ให้แสดงภาพ(หน้าจอกล้อง)จาก frame และ ถ้าภาพแสดงได้ ให้รอการป้อนค่าจากคีย์บอร์ด (ซึ่งผมตั้งให้กด z เพื่อปิดการแสดงภาพ)
    if check == True:
        cv2.imshow("Video", frame)
        if cv2.waitKey(1) & 0xFF == ord('z'):
            break
    else:
        break

# ปล1.เหตุผลที่สามารถแยกมือซ้ายและมือขวาออกจากกันได้นั้น เป็นเพราะการใช้ตำแหน่งของ "โคนนิ้วกลาง(ตำแหน่งที่ 9)" เปรียบเทียบกับ "โคนนิ้วนาง(ตำแหน่งที่ 13)"        ถ้าตำแหน่งที่ 9 มีค่ามากกว่าตำแหน่งที่ 13 นั่นคือมือขวา แต่ถ้าตำแหน่งที่ 13 มากกว่าตำแหน่งที่ 9 นั่นคือมือซ้าย
# ปล2.การเปรียบเทียบค่าจากโคนนิ้วที่ทำใน Code นี้สามารถเปลี่ยนไปใช้นิ้วในตำแหน่งอื่นเพื่อเปรียบเทียบได้ว่าเป็นมือซ้ายหรือมือขวาได้
# ปล3. การเปรียบเทียบค่าจากโคนนิ้วที่ทำใน Code นี้เมื่อพลิกมือจากหน้ามือเป็นหลังมือจะไม่สามารถแสดงค่าได้ตรง เช่น                                                   ถ้าชูมือขวา ข้อความที่แสดงจะเป็นไปตามปกตินั่นก็คือแสดงค่าตามนิ้วมือที่โชว์ในข้างขวา แต่เมื่อพลิกมือข้อความที่แสดงจะเปลี่ยนจากขวาเป็นซ้าย