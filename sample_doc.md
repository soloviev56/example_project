### Сравнение модели тонкого слоя со сферическими включениями с объемными моделями

В разделе 2.3 статьи рассматривается модель эффективной теплопроводности тонкого слоя с редкими сферическими включениями. Для сравнения рассмотрим классические объемные модели, приведённые в файле "Объемные_Модели.pdf":

- **Логарифмический закон смешения**:  
  $$\lambda_e = \lambda_m^{1-\varphi} \lambda_f^{\varphi}$$
- **Модель Миснара**:  
  $$\frac{\lambda_e}{\lambda_m} = 1 + \frac{\varphi (1 - \lambda_m/\lambda_f)}{1 - \varphi^{1/3} + \lambda_m/\lambda_f - \lambda_m}$$
- **Формула Максвелла**:  
  $$\lambda_e = \lambda_m \frac{\lambda_f + 2\lambda_m + 2\varphi(\lambda_f - \lambda_m)}{\lambda_f + 2\lambda_m - \varphi(\lambda_f - \lambda_m)}$$
- **Модель тонкого слоя (статья)**:  
  $$\lambda_e = \lambda_m + (\lambda_f - \lambda_m)\varphi$$  
  Здесь $$\varphi$$ — объемная доля включений, $$\lambda_m$$ — теплопроводность матрицы, $$\lambda_f$$ — теплопроводность включений.

### Программа для построения зависимостей

```python
import numpy as np
import matplotlib.pyplot as plt

# Диапазон объемной доли включений
phi = np.linspace(0, 0.2, 100)
lambda_m = 1.0  # теплопроводность матрицы
lambda_f = 5.0  # теплопроводность включения

# Модели
lambda_log = lambda_m**(1-phi) * lambda_f**phi
lambda_misnar = lambda_m * (1 + phi * (1 - lambda_m/lambda_f) / (1 - phi**(1/3) + lambda_m/lambda_f - lambda_m))
lambda_maxwell = lambda_m * (lambda_f + 2*lambda_m + 2*phi*(lambda_f - lambda_m)) / (lambda_f + 2*lambda_m - phi*(lambda_f - lambda_m))
lambda_thin_layer = lambda_m + (lambda_f - lambda_m) * phi

plt.figure(figsize=(8,5))
plt.plot(phi, lambda_log, label='Логарифмический закон')
plt.plot(phi, lambda_misnar, label='Модель Миснара')
plt.plot(phi, lambda_maxwell, label='Формула Максвелла')
plt.plot(phi, lambda_thin_layer, label='Модель тонкого слоя')
plt.xlabel('Объемная доля включений, φ')
plt.ylabel('Эффективная теплопроводность, λ_e')
plt.legend()
plt.grid(True)
plt.title('Зависимость λ_e от φ')
plt.show()

# Зависимость от теплопроводности включения при фиксированной φ
phi_fixed = 0.1
lambda_f_range = np.linspace(0.1, 10, 200)
lambda_log_fixed = lambda_m**(1-phi_fixed) * lambda_f_range**phi_fixed
lambda_misnar_fixed = lambda_m * (1 + phi_fixed * (1 - lambda_m/lambda_f_range) / (1 - phi_fixed**(1/3) + lambda_m/lambda_f_range - lambda_m))
lambda_maxwell_fixed = lambda_m * (lambda_f_range + 2*lambda_m + 2*phi_fixed*(lambda_f_range - lambda_m)) / (lambda_f_range + 2*lambda_m - phi_fixed*(lambda_f_range - lambda_m))
lambda_thin_layer_fixed = lambda_m + (lambda_f_range - lambda_m) * phi_fixed

plt.figure(figsize=(8,5))
plt.plot(lambda_f_range, lambda_log_fixed, label='Логарифмический закон')
plt.plot(lambda_f_range, lambda_misnar_fixed, label='Модель Миснара')
plt.plot(lambda_f_range, lambda_maxwell_fixed, label='Формула Максвелла')
plt.plot(lambda_f_range, lambda_thin_layer_fixed, label='Модель тонкого слоя')
plt.xlabel('Теплопроводность включения, λ_f')
plt.ylabel('Эффективная теплопроводность, λ_e')
plt.legend()
plt.grid(True)
plt.title('Зависимость λ_e от λ_f при φ=0.1')
plt.show()
```

### Обсуждение результатов

- **Линейность модели тонкого слоя**:  
  Модель тонкого слоя предсказывает линейный рост эффективной теплопроводности с увеличением доли включений, что хорошо согласуется с физическим смыслом при малых $$\varphi$$. Это отражает тот факт, что вклад редких включений пропорционален их объему.

- **Объемные модели**:  
  - **Максвелл** и **логарифмический закон** дают более сложную, но плавную зависимость, учитывая взаимодействие между включениями.  
  - При малых $$\varphi$$ все модели сходятся, но с ростом $$\varphi$$ различия увеличиваются: объемные модели учитывают нелинейные эффекты и насыщение.
  - **Модель Миснара** близка к логарифмической и Максвеллу при малых долях включений.

- **Зависимость от теплопроводности включения**:  
  - Все модели показывают рост $$\lambda_e$$ с увеличением $$\lambda_f$$, но насыщение (замедление роста) выражено только в объемных моделях.
  - Модель тонкого слоя сохраняет линейную зависимость по $$\lambda_f$$ при фиксированной $$\varphi$$, что является приближением, справедливым для разреженных включений.

- **Физический смысл**:  
  Модель тонкого слоя применима для тонких покрытий с редкими крупными включениями, где объемная доля мала и взаимодействием между включениями можно пренебречь. При увеличении $$\varphi$$ или для плотных композитов предпочтительнее использовать объемные модели, такие как формула Максвелла.

**Вывод:**  
Модель тонкого слоя со сферическими включениями хорошо описывает поведение эффективной теплопроводности при малых объемных долях включений и служит удобным аналитическим приближением. Для более высоких концентраций и сложных композитов необходимо использовать объемные модели, учитывающие взаимодействие между включениями и нелинейные эффекты[1][2].

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/63199/3934bd27-52ad-4f16-95d9-8c606dd28218/article_PNRPU.pdf
[2] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/63199/7677eef1-ede9-4567-b382-8c079e121fc2/Obemnye_Modeli.pdf
