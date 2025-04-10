
1) Blinking LED: Toggle-Delay

In the main loop, insert the following:

HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5); //Turn PIN from ON to OFF, or from OFF to ON (PINs' names and where they lead, along with what ports they have, can be found from documentation [*board model* datasheet, search it on Google])
HAL_Delay(1000); //wait 1000ms = 1s before restarting the loop



2) Blinking LED: Using a timer

From CubeMX:

On the left, select the timer section, then choose a general purpose timer (can be seen when hovering mouse on it).
Now on the timer, select the following settings:
-Clock source: Internal Timer
-TIMX Global Interrupt: Enabled [can be found under "NVIC Settings"]

Also, in the Parameter Settings, the Prescaler and Period need to be set, but what are they?
The prescaler is *FILL IT OUT AT ANOTHER TIME*. For now, set it to 16000 - 1, which (considering a clock of 16MHz) will lead to a tick of 1ms.
The period is *FILL IT OUT AT ANOTHER TIME*. For now, set it 1000, which (considering a tick of 1ms) will lead to an interrupt every second.

Start the timer adding, in main.c (inside //USER CODE BEGIN 2):

HAL_TIM_Base_Start_IT(&htimX);

void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypedDef *htim) {
  HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
}



3) Blinking LED: Output Compare

Write, in main.c:

HAL_TIM_OC_Start_IT(&htim2, TIM_CHANNEL_1); (inside //USER CODE BEGIN 2)

In CubeMX, modify your timer as follows:
-Channel1: Output Compare CH1
-Output Compare Channel 1, Mode: Toggle on match [can be found under "Parameter Settings"]

