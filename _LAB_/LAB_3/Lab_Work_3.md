## **Лабораторна робота № 3**
# **Просторова обробка зображень. Фільтрація зображень.**
- - -
## **Мета роботи:**
Ознайомитись базовими алгоритмами просторової обробки зображень за допомогою фільтрів

## **Засоби виконання роботи:**
Для виконання роботи можливо використовувати довільний iнтерпретатор мови [PYTHON](https://www.python.org/downloads/), також [IDE Anaconda](https://anaconda.org/) (Jupyter Lab / Jupyter Notebook, Spyder) або [Microsoft Visual Studio](https://visualstudio.microsoft.com).

## **Теоретичні відомості**

## **Завдання до виконання**
1. Зчитати оригінальне зображення у відповідності за варіантом завдання лабораторної роботи №1.
1. Вивести структуру та розмір орігінального зображення.
1. Сформувати  розмите зображення за допомогою гаусова фільтра. Зберігти у файл в форматі BMP.
1. Сформувати  зображення з підвищеною різкістю за допомогою ???? фільтра. Зберігти у файл в форматі BMP.
1. За допомогою фільтру Собеля Сформувати  зображення з віділенням меж. Зберігти у файл в форматі BMP.
1.  



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



- ### **Повний приклад програм дивись** [Lab3.1](Lab_2_Example_1.ipynb), [Lab2.2](Lab_2_Example_2.ipynb), [Lab3.3](Lab_2_Example_1.ipynb) 
