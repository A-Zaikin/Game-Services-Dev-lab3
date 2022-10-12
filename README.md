# РАЗРАБОТКА ИГРОВЫХ СЕРВИСОВ
### Ссылка на проект: https://github.com/A-Zaikin/DragonPicker
Отчет по лабораторной работе #2 выполнил:
- Заикин Александр Юрьевич
- РИ300012
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | # | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Создание интерактивного приложения с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.

## Задание 1
### Используя видео-материалы практических работ 1-5 повторить реализацию игровых механик.
Ход работы:
#### Работа 1: «Механизм ловли объектов»
1)	Добавить в EnergyShield скрипт движения:
```cs
using UnityEngine;

namespace DragonPicker
{
    [RequireComponent(typeof(Rigidbody))]
    public class EnergyShieldMovement : MonoBehaviour
    {
        [SerializeField] private float speedMultiplier;

        private Vector3 mousePosition;
        private new Rigidbody rigidbody;

        private void Awake()
        {
            rigidbody = GetComponent<Rigidbody>();
        }

        private void Update()
        {
            mousePosition = Input.mousePosition;
        }

        private void FixedUpdate()
        {
            var distanceToCamera = transform.position.z - Camera.main.transform.position.z;
            var relativeMousePosition = mousePosition + distanceToCamera * Vector3.forward;
            var goalPosition = Camera.main.ScreenToWorldPoint(relativeMousePosition);
            rigidbody.AddForce((goalPosition.x - transform.position.x) * speedMultiplier * Vector3.right);
        }
    }
}
```

2) Поставить префабу яица тег Dragon Egg.
3) Изменить код яица, чтобы он сам взрывался только об землю.
4) Добавить в EnergyShield скрипт подбора яица:
```cs
using UnityEngine;

namespace DragonPicker
{
    [RequireComponent(typeof(Collider))]
    public class EnergyShieldCollision : MonoBehaviour
    {
        [SerializeField] private GameObject effectPrefab;

        private void OnCollisionEnter(Collision collision)
        {
            var effect = Instantiate(effectPrefab, transform);
            effect.transform.position = collision.GetContact(0).point;

            if (collision.gameObject.CompareTag("Dragon Egg"))
            {
                Destroy(collision.gameObject);
            }
        }
    }
}
```
5) Добавить в Canvas новый TextField для счёта, расположить его в правом верхнем углу экрана.
   
!["screenshot"](Screenshots/1.webp)



## Задание 2
### В проект, выполненный в предыдущем задании, добавить систему проверки того, что SDK подключен (доступен в режиме онлайн и отвечает на запросы)
Ход работы:





## Выводы

Изучил процесс создания интерактивного приложения и принципы интеграции в него игровых сервисов. Познакомился с работой на платформе Yandex Игры.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
