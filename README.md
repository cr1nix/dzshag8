import time

def measure_time(func):

    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        elapsed_time = end_time - start_time
        print(f"Функція {func.__name__} виконалась за {elapsed_time:.6f} секунд")
        return result
    return wrapper


@measure_time
def slow_function(seconds):

    time.sleep(seconds)
    return f"Працювала {seconds} секунд"


def test_measure_time():
    @measure_time
    def add_numbers(a, b):
        return a + b

    result1 = add_numbers(3, 5)
    assert result1 == 8, "Тест 1 не пройдено!"

    @measure_time
    def multiply_numbers(a, b):
        return a * b

    result2 = multiply_numbers(4, 6)
    assert result2 == 24, "Тест 2 не пройдено!"


    result3 = slow_function(1)
    assert result3 == "Працювала 1 секунд", "Тест 3 не пройдено!"


if __name__ == "__main__":
    test_measure_time()
