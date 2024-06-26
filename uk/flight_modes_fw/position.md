# Режим позиції (фіксоване крило)

<img src="../../assets/site/difficulty_easy.png" title="Easy to fly" width="30px" />&nbsp;<img src="../../assets/site/remote_control.svg" title="Необхідний ручний/дистанційний пульт" width="30px" />&nbsp;<img src="../../assets/site/position_fixed.svg" title="Position fix required (e.g. GPS)" width="30px" />

_Режим позиції_ є найлегшим і найбезпечнішим ручним режимом. Підтримується на транспортних засобах, які мають прогноз позиціонування (наприклад, GPS). Це полегшує пілотам контроль висоти транспортного засобу, і зокрема досягати і підтримувати фіксовану висоту. Режим буде утримувати курс транспортного засобу від вітру. Швидкість активно контролюється, якщо встановлений датчик швидкості.

Транспортний засіб виконує [координований поворот](https://en.wikipedia.org/wiki/Coordinated_flight), якщо рулі не нульові, тоді як pitch -стік контролює швидкість підйому/спуску. Засувка визначає швидкість — при 50% засувки літак буде утримувати свою поточну висоту з заданою крейсерською швидкістю.

Коли всі стіки управління відпущені/центровані (без крену, тангажу, курсу та близько 50% керування газом), літак повернеться до прямого, рівного польоту та збереже свою поточну висоту та траєкторію польоту не залежно від вітру. This makes it easy to recover from any problems when flying. Крен та тангаж - кутово-керовані (тому неможливо перевалюватися або робити петлю транспортному засобу).

Стік повороту може бути використана для збільшення/зменшення кута рискання при поворотах. Якщо контролер фіксований у центрі, то він самостійно здійснює координацію повороту, що означає, що він застосовує необхідну швидкість розвороту для поточного кута крену, щоб виконати плавний поворот. Діаграма нижче візуально показує поведінку режиму (для [передавача режиму 2](../getting_started/rc_transmitter_receiver.md#transmitter_modes)).

![FW Position Mode](../../assets/flight_modes/position_fw.png)

## Технічний опис

Режим позиції, як [Режим стабілізації](../flight_modes_fw/altitude.md), але зі стабілізацією курсу. Швидкість також стабілізується, якщо встановлений датчик швидкості.

- Центровані вхідні показники крену/тангажу/рискання (в межах дедбенду):
  - Автопілот рівномірно підтримує транспортний засіб і утримує висоту, швидкість і курс над землею.
- Зовнішній центр:
  - Стік регулює висоту польоту.
  - Резервний стік керує швидкістю літального апарату, якщо підключений датчик швидкості. Без датчика швидкості, транспортний засіб летітиме прямо на малому газу ([FW_THR_TRIM](../advanced_config/parameter_reference.md#FW_THR_TRIM)), збільшуючи або зменшуючи газ у міру необхідності для підйому або спуску.
  - Стік керування використовує кут крена. Автопілот буде підтримувати [координований польот](https://en.wikipedia.org/wiki/Coordinated_flight).
  - Стік крену додає додатковий значення швидкості рискання (додається до розрахованого автопілотом для підтримки координованого польоту). Може бути використаний для ручної зміни кута рискання безпілотного засобу.
- Потрібен ручний ввід управління (наприклад, за допомогою пульта дистанційного керування, джойстика).
- Необхідний пристрій вимірювання висоти (зазвичай барометр або GPS)

## Параметри

На режим впливають наступні параметри:

| Параметр                                                                                                    | Опис                                                                                               |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| <a id="FW_AIRSPD_MIN"></a>[FW_AIRSPD_MIN](../advanced_config/parameter_reference.md#FW_AIRSPD_MIN)         | Мінімальна швидкість. За замовчуванням: 10 м/с.                                                    |
| <a id="FW_AIRSPD_MAX"></a>[FW_AIRSPD_MAX](../advanced_config/parameter_reference.md#FW_AIRSPD_MAX)         | Максимальна швидкість. За замовчуванням: 20 м/с.                                                   |
| <a id="FW_AIRSPD_TRIM"></a>[FW_AIRSPD_TRIM](../advanced_config/parameter_reference.md#FW_AIRSPD_TRIM)       | Крейсерська швидкість. За замовчуванням: 15 м/с.                                                   |
| <a id="FW_MAN_P_MAX"></a>[FW_MAN_P_MAX](../advanced_config/parameter_reference.md#FW_MAN_P_MAX)           | Установлення максимального кроку в режимі стабілізації кута нахилу. За замовчуванням: 45 градусів. |
| <a id="FW_MAN_R_MAX"></a>[FW_MAN_R_MAX](../advanced_config/parameter_reference.md#FW_MAN_R_MAX)           | Максимальне значення крена в режимі стабілізації кута нахилу. За замовчуванням: 45 градусів.       |
| <a id="FW_T_CLMB_R_SP"></a>[FW_T_CLMB_R_SP](../advanced_config/parameter_reference.md#FW_T_CLMB_R_SP)     | Максимальна задана швидкість підйому. За замовчуванням: 3 м/с.                                     |
| <a id="FW_T_SINK_R_SP"></a>[FW_T_SINK_R_SP](../advanced_config/parameter_reference.md#FW_T_SINK_R_SP)     | Максимальне значення зниження швидкості. За замовчуванням: 2 м/с.                                  |
| <a id="FW_PN_R_SLEW_MAX"></a>[FW_PN_R_SLEW_MAX](../advanced_config/parameter_reference.md#FW_PN_R_SLEW_MAX) | Обмеження швидкості нахилу вихідного значення. За замовчуванням: 90 °/с.                           |
