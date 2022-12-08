# Practicum 2 - Numerical Computation

Name           : Rafi Aliefian Putra Ramadhani        
NRP            : 5025211234
Kelompok       : C11 (Alya Putri Salma, Kartika Diva Asmara Gita)

## Source Code with Python (Py)

```R
import numpy as np
import math 

def f(x):
    return math.sin(x)

def CompTrapzRule (points: np.ndarray) -> float:
    h = points[1] - points[0]
    if(points.size < 2): 
        return -1
    else:
        temp = 0
        for i in range(1, points.size - 1):
            temp += f(points[i])
        return h / 2 * (f(points[0]) + 2 * temp + f(points[points.size - 1]))

def romberg(a, b, iterasi):
    matrix = [] #untuk menyimpan nilai romberg
    for _ in range(0, iterasi): 
        matrix.append([None for _ in range(0, iterasi)])
    
    section = 1 #jumlah untuk Composite Trapezoid Rule
    iteration = 0 #awal iterasi dari perulangan while
    while (section < 2**iterasi):
        points = np.linspace(a, b, section + 1) #untuk mendapatkan poin tersebar merata
        matrix[iteration][0] = CompTrapzRule (points) 

        section *= 2
        iteration += 1
    
    #menghitung integrasi romberg
    for i in range(1, iterasi):
        for j in range(1, iterasi):
            if (i < j):
                continue
            
            #rumus romberg
            temp = (4*(j) * matrix[i][j - 1] - matrix[i - 1][j - 1]) / (4*(j) - 1)
            matrix[i][j] = temp

    return matrix[iterasi - 1][iterasi - 1]
    
def main():
    a = 0  #batas bawah    
    b = math.pi #batas atas
    iterasi = 9    

    hasil = romberg(a, b, iterasi)
    print("Romberg ({},{}) = {}".format(iterasi, iterasi, hasil))
if __name__ == "__main__":
    main()
```

## Output Program :
![pr2](https://user-images.githubusercontent.com/91828276/206484653-35674f18-4a84-427e-8807-96b724051b9a.png)
</br>
 - Thank you Numerical Computation - 
