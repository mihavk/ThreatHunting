
# Основы обработки данных с помощью R

# Практика 1

## Цель работы
### 1. Развить практические навыки использования языка программирования R для обработки данных
### 2. Закрепить знания базовых типов данных языка R
### 3. Развить пркатические навыки использования функций обработки данных пакета dplyr – функции select(), filter(), mutate(), arrange(), group_by()


## Выводим датасет
```{r}
library(dplyr)
starwars_data <- starwars

starwars_data
```

## Задание 1. Сколько строк в датафрейме
```{r}
nrow(starwars_data)
```

## Задание 2. Сколько столбцов в датафрейме?
```{r}
ncol(starwars_data)
```

## Задание 3. Как посмотреть примерный вид даатфрейма?
```{r}
glimpse(starwars_data)
```

## Задание 4. Сколько уникальных рас персонажей (species) представлено в данных?
```{r}
x <- starwars$species %>% unique()
length(x)
```

## Задание 5. Найти самогго высокого персонажа
```{r}
max_height <- which.max(starwars_data$height)
max_height
starwars_data[which.max(starwars_data$height),]$name
```

## Задание 6. Найти всех персонажей ниже 170
```{r}
starwars_data %>% filter(height <= 170)
```

## Задание 7. Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать по формуле 𝐼 = 𝑚 /ℎ2 , где 𝑚– масса (weight), а ℎ – рост (height)
```{r}
item <- (starwars_data$height) / (starwars_data$mass)
item

```

## Задание 8. Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей
```{r}
max_imt <- sort(item,decreasing = TRUE)
max_imt[1:10]
```

## Задание 9. Найти средний возраст персонажей каждой расы вселенной Звездных войн
```{r}
library(tidyverse)
starwars_data %>%
  drop_na() %>%
  group_by(species) %>%
  summarise(
    'mean height' = mean(height)
  )
```

## Задание 10. Найти самый распространенный цвет глаз персонажей вселенной Звездных войн
```{r}
a1 <- c(count(starwars_data,eye_color))
print (a1[["eye_color"]][which.max(unlist(a1["n"]))])



```

## Задание 11. Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.
```{r}
require(stringi)
starwars_data$species[is.na(starwars_data$species)] <- "Unknown"

for (x in unique(starwars_data$species)) {
  print(paste(x, ":",mean(stri_length(starwars_data$name)[starwars_data$species == x])))
}
```







