# day13
import itertools

# 연산 함수 정의
def calc(a, b, op):
    if op == '+':
        return a + b
    elif op == '-':
        return a - b
    elif op == '*':
        return a * b
    elif op == '/':
        if a * b < 0:
            return -(abs(a) // abs(b))  # C++14의 부호 규칙
        return a // b

# 백트래킹 방식으로 연산자 배열을 적용하여 계산하는 함수
def calculate(arr, ops):
    result = arr[0]
    index = 1
    for op in ops:
        result = calc(result, arr[index], op)
        index += 1
    return result

# 주어진 수와 연산자 개수로 최대, 최소값을 찾는 함수
def find_max_min(N, A, op_count):
    operators = []
    
    # 연산자 리스트 만들기
    operators += ['+'] * op_count[0]
    operators += ['-'] * op_count[1]
    operators += ['*'] * op_count[2]
    operators += ['/'] * op_count[3]

    max_value = -float('inf')
    min_value = float('inf')

    # 연산자들의 모든 순열을 계산하여 각 경우의 결과를 구함
    for ops in set(itertools.permutations(operators)):  # 중복되는 순열을 피하기 위해 set 사용
        result = calculate(A, ops)
        max_value = max(max_value, result)
        min_value = min(min_value, result)

    return max_value, min_value

# 입력 받기
N = int(input())  # 수의 개수
A = list(map(int, input().split()))  # 수열
op_count = list(map(int, input().split()))  # 연산자 개수 [+, -, *, /]

# 결과 출력
max_value, min_value = find_max_min(N, A, op_count)
print(max_value)
print(min_value)
