import random

class Car:
    def __init__(self, name, speed):
        self.name = name
        self.speed = speed

    def accelerate(self):
        self.speed += random.randint(1, 5)

    def brake(self):
        self.speed -= random.randint(1, 3)

    def display_speed(self):
        return f"{self.name}의 속도: {self.speed}"

def main():
    player_car = Car("Player Car", 0)
    opponent_car = Car("Opponent Car", 0)

    distance = 0
    while distance < 100:
        player_choice = input("가속하려면 'a', 브레이크를 사용하려면 'b'를 누르세요: ")

        if player_choice == 'a':
            player_car.accelerate()
        elif player_choice == 'b':
            player_car.brake()
        else:
            print("잘못된 입력입니다. 다시 시도하세요.")
            continue

        opponent_car.accelerate()

        print(player_car.display_speed())
        print(opponent_car.display_speed())

        distance += max(player_car.speed - opponent_car.speed, 0)
        print(f"현재 거리: {distance}m")

        if distance >= 100:
            print("축하합니다! 당신이 이겼습니다!")
        elif player_car.speed <= 0:
            print("당신의 자동차가 멈췄습니다. 게임 종료!")
            break

if __name__ == "__main__":
    main()
