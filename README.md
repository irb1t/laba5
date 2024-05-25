# laba5
Задана рекуррентная функция. Область определения функции – натуральные числа.
Написать программу сравнительного вычисления данной функции рекурсивно и итерационно.
Определить границы применимости рекурсивного и итерационного подхода.
Результаты сравнительного исследования времени вычисления представить в табличной и графической форме в виде отчета по лабораторной работе.


30.	F(1) = 2; G(1) = 1; F(n) = (-1)n*(G(n–2)/(3n)!, G(n) = F(n–2), при n >=2








def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n - 1)

def F_recursive(n):
    if n == 1:
        return 2
    else:
        return ((-1)**n * G_recursive(n - 2)) / (3 * factorial(n))

def G_recursive(n):
    if n == 1:
        return 1
    else:
        return F_recursive(n - 2)
def F_iterative(n):
    if n == 1:
        return 2
    f = [2]  # F(1) = 2
    g = [1]  # G(1) = 1
    for i in range(2, n + 1):
        f.append(((-1)**i * g[i - 2]) / (3 * factorial(i)))
        g.append(f[i - 2])
    return f[-1]

def G_iterative(n):
    if n == 1:
        return 1
    f = [2]  # F(1) = 2
    g = [1]  # G(1) = 1
    for i in range(2, n + 1):
        f.append(((-1)**i * g[i - 2]) / (3 * factorial(i)))
        g.append(f[i - 2])
    return g[-1]
import time
import matplotlib.pyplot as plt

def measure_time(func, n):
    start_time = time.time()
    result = func(n)
    end_time = time.time()
    return end_time - start_time, result

def compare_methods(max_n):
    recursive_times = []
    iterative_times = []
    ns = list(range(1, max_n + 1))
    
    for n in ns:
        rec_time, _ = measure_time(F_recursive, n)
        itr_time, _ = measure_time(F_iterative, n)
        recursive_times.append(rec_time)
        iterative_times.append(itr_time)
    
    return ns, recursive_times, iterative_times

max_n = 20  # Можно изменить для тестирования границ применимости
ns, recursive_times, iterative_times = compare_methods(max_n)

# Табличное представление результатов
print("n\tRecursive Time\tIterative Time")
for i in range(len(ns)):
    print(f"{ns[i]}\t{recursive_times[i]:.6f}\t{iterative_times[i]:.6f}")

# Графическое представление результатов
plt.figure(figsize=(12, 6))
plt.plot(ns, recursive_times, label='Recursive Time')
plt.plot(ns, iterative_times, label='Iterative Time')
plt.xlabel('n')
plt.ylabel('Time (seconds)')
plt.title('Recursive vs Iterative Time Complexity')
plt.legend()
plt.grid(True)
plt.show()
