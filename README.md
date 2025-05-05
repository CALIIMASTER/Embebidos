# Embebidos
Trabajos embebidos

from machine import mem32
from uctypes import addressof
import array

def bezier(p0,p1,p2,p3,n):
    p_0 = array.array('l', [p0[0][0], p0[1][0]])
    p_1 = array.array('l', [p1[0][0], p1[1][0]])
    p_2 = array.array('l', [p2[0][0], p2[1][0]])
    p_3 = array.array('l', [p3[0][0], p3[1][0]])
    dir_p0=addressof(p_0)
    dir_p1=addressof(p_1)
    dir_p2=addressof(p_2)
    dir_p3=addressof(p_3)
    print("dir_p0: ",[[mem32[dir_p0]],[mem32[dir_p0+4]]])
    print("dir_p1: ",[[mem32[dir_p1]],[mem32[dir_p1+4]]])
    print("dir_p2: ",[[mem32[dir_p2]],[mem32[dir_p2+4]]])
    print("dir_p3: ",[[mem32[dir_p3]],[mem32[dir_p3+4]]])
    
    LR=[]
    for i in range(n+1):
        t = i / n
        x = ((1 - t)**3 * mem32[dir_p0] + 3 * (1 - t)**2 * t * mem32[dir_p1] +3 * (1 - t) * t**2 * mem32[dir_p2] + t**3 * mem32[dir_p3])

        y = ((1 - t)**3 * mem32[dir_p0+4] + 3 * (1 - t)**2 * t * mem32[dir_p1+4] + 3 * (1 - t) * t**2 * mem32[dir_p2+4] + t**3 * mem32[dir_p3+4])
        LR.append([[x], [y]])
        
    return LR


p0 = [[6], [1]]
p1 = [[50], [150]]
p2 = [[100], [158]]
p3 = [[200], [0]]
n = 4


resultado = bezier(p0, p1, p2, p3, n)

for j in range(len(resultado)):
    print('LR[',j,']=',resultado[j])
