## **Лабораторна робота № 2**
# **Просторова обробка зображень. Перетворення яскравості та контрасту**

- - -
## **Мета роботи:**
Ознайомитись базовими алгоритмами просторової обробки зображень за допомогою амплітудних перевореннь

## **Засоби виконання роботи:**
Для виконання роботи можливо використовувати довільний iнтерпретатор мови [PYTHON](https://www.python.org/downloads/), також [IDE Anaconda](https://anaconda.org/) (Jupyter Lab / Jupyter Notebook, Spyder) або [Microsoft Visual Studio](https://visualstudio.microsoft.com).

## **Теоретичні відомості**

## **Завдання до виконання**
1. Зчитати оригінальне зображення у відповідності за варіантом завдання лабораторної роботи №1.
1. Вивести структуру та розмір орігінального зображення.
1. Сформувати напівтонове зображення з орігінального зображення. Зберігти у файл в форматі BMP.
1. Сформувати негативне зображення з орігінального напівтонового зображення. Зберігти у файл в форматі BMP.
1. Змінити яскравість зображення (зміщення відповідно варіанту). Вивести на екран. Зберігти у файл в форматі BMP.
1. Змінити контраст зображення (зміщення парметри гамма функції відповідно варіанту). Вивести на екран. Зберігти у файл в форматі BMP.
1. Сформувати гістограму зображення. Вивести на екран.
1. Сформувати нормалізоване зображення №2. Вивести на єкран. Зберігти у файл в форматі BMP.
1. Вивести на екран порівняння гістограми орігігального та нормалізованого зображень.

## **Варіанти завдання**
|Варіант|[Файл Зображення](https://github.com/eabshkvprof/2020_Digita_Image_Processing/tree/master/Test_Images)|L_bias| L_low | L_top|
|:-------|:-------|:----- |:---|:--|
|**1**|COCO_000012774.jpg  |25|25|225|
|**2**|COCO_000015322.jpg  |50|35|200|
|**3**|COCO_000025391.jpg  |75|45|175|
|**4**|COCO_000028877.jpg  |80|55|225|
|**5**|COCO_000040672.jpg  |50|65|225|
|**6**|COCO_000049940.jpg  |40|75|175|
|**7**|COCO_000104571.jpg  |-90|85|225|
|**8**|COCO_000112142.jpg  |-100|40|200|
|**9**|COCO_000117357.jpg  |-85|50|200|
|**10**|COCO_000170013.jpg  |-65|60|225|
|   | |   |
|**21**|COCO_000173164.jpg |25|25| 225|
|**22**|COCO_000176388.jpg |50|25| 200|
|**23**|COCO_000180783.jpg |75|25| 180|
|**24**|COCO_000186732.jpg |85|25| 225|
|**26**|COCO_000224540.jpg |100|25| 200|
|**27**|COCO_000277143.jpg |90|25| 180|
|**28**|COCO_000286630.jpg |-30|25| 225|
|**29**|COCO_000366557.jpg |-40|25| 200|
|**30**|COCO_000390755.jpg |-60|25| 180|
|**31**|COCO_000411389.jpg |-70|25| 200|
|**32**|COCO_000495977.jpg |-50|25| 180|



## **Приклади**
- ### **Побудова напівтогнованого зображення та негативного зображення**
Вважаємо, що орігінальне зображення завантажено до масиву ***test_image*** та визначені змінні ***rows_num*** , ***clms_num***
```
## Визначення масиву НАПІВТТОНОВОГО зображення
gray_image = np.zeros ( (rows_num, clms_num, 3), dtype=np.uint8)
## Визначення масиву НЕГАТИВНОГО НАПІВТТОНОВОГО зображення
gray_im_neg = np.zeros ( (rows_num, clms_num, 3), dtype=np.uint8)
print ('Gray_Im SAPE', gray_im.shape, 'Gray_Im SIZE', rows_num * clms_num)
for i in  range (rows_num):
    for j in  range (clms_num):
        # Gray image
        gray_image[i, j, :] = 0.299*test_image[i,j,0]+0.587*test_image[i,j,1]+0.114*test_image[i,j,2]
        gray_im_neg[i,j,:] = 256-gray_im [i, j, 0]       
## СУМІСНИЙ ВИВІД НАПІВТОНОВАНОГО та НЕГАТИВНОГО НАПІВТОНОВАНОГО зображення
fig, axes = plt.subplots(1, 2, figsize=(16, 8))
ax = axes.ravel()
ax[0].imshow(gray_im)
ax[0].set_title("Original Gray")
ax[1].imshow(gray_im_neg)
ax[1].set_title("Negativ Gray")
plt.show()
```

- ### **Керування яскравістю зображення**
Вважаємо, що орігінальне напівтонове зображення завантажено до масиву ***gray_image*** та визначені змінні ***rows_num*** , ***clms_num***
Зміщення яскравостей зображення визначається значенням змінної ***L_bias***, 0<L_bias< 256
```
L_min =  np.amin(gray_im)
L_max =  np.amax(gray_im)
L_bias = 50
print ('Luminance MIN = ', L_min, 'Luminance MAX = ',L_max, 'Luminance Bias = ',L_bias)
## Визначення масиву зображення з півищеною яскравістю
gray_im_L = np.zeros ( (rows_num, clms_num, 3), dtype=np.uint8)
for i in  range (rows_num):
    for j in  range (clms_num):
        L = gray_im [i, j, 0] + L_bias
        if L < 0:
            gray_im_L [i, j, :] = 0
        elif L>bins-1:
            gray_im_L [i, j, :] = bins-1
        else :    
            gray_im_L [i, j, :] = L
```
- ### **Керування контрастом зображення**
Вважаємо, що орігінальне напівтонове зображення завантажено до масиву ***gray_image*** та визначені змінні ***rows_num*** , ***clms_num***  
В прикладі гамма функція визначається наступним чином: всі пікселі зображення, яскравість яких меньш ***L_low*** вважаються чорними (значення 0), всі пікселі, яскравість яких більш  ***L_top*** вважаються білими (значення 255). Яскравість останніх пікселів "розтягується" від 0 до 255.
```
## Визначення масиву зображення з півищеним контрастом
gray_im_С = np.zeros ( (rows_num, clms_num, 3), dtype=np.uint8)
## Визначення ГАММА функції
Gamma = np.zeros ( (bins, 3), dtype=np.float32)
## Найпростіша ГАММА функція підвіщення контрасту
L_low  = 50
L_top  = 200
K = bins/(L_top-L_low)
for i in range(bins):
    if i < L_low:
        Gamma[i]=0
    elif i>L_top:
        Gamma[i]=bins-1
    else :
        Gamma[i]=K
for i in  range (rows_num):
    for j in  range (clms_num):
        gray_im_С[i,j,:]=Gamma[gray_image[i,j,0]]*gray_im[i,j,0]
```

- ### **Побудова гістограми**
Вважаємо, що напівтоноване  завантажено до масиву ***gray_image*** та визначені змінні ***rows_num*** , ***clms_num***, ***bins***
```
## Визначення масиву для гістограми
L_gisto = np.zeros ((bins), dtype=np.uint32)
for i in  range (rows_num):
    for j in  range (clms_num):
        # Формування гістограми
        L_gisto[gray_image [i, j, 0]] += 1
## Вивід гістограми
pix_index = np.arange(256)
fig, ax = plt.subplots(figsize=(8,8))
plt.title('GISTOGRAM')
ax.bar(pix_index, L_gisto)
plt.show()        
```
- ### **Нормалізація гістограми та зображення**
Вважаємо, що напівтоноване  завантажено до масиву ***gray_image*** та визначені змінні ***rows_num*** , ***clms_num***. Також визначена гістограма зображення ***L_gisto***
```
## Нормалізування гістограми
Norm_L_gisto = np.zeros ( (256), dtype=np.float32)
Norm_L_gisto [:] =  255.0*L_gisto[:]/pix_num
norm_sum = np.sum(Norm_L_gisto)
## Кумулятивна гістограма
Cum_gisto = np.zeros ( (256), dtype=np.float32)
for i in  range (bins):
    Cum_gisto[i] = np.sum(Norm_L_gisto[0:i])
## Нормалізоване зображення
norm_image = np.zeros ( (rows_num, clms_num, 3), dtype=np.uint8)    
for i in  range (rows_num):
    for j in  range (clms_num):
        # Gray image
        norm_image [i, j, : ] = Cum_gisto[image_gray_channal[i,j]]
```

- ### **Повний приклад програм дивись** [Lab2.1](Lab_2_Example_1.ipynb), [Lab2.2](Lab_2_Example_2.ipynb)
