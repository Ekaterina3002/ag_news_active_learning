# ag_news_active_learning

## описание набора данных:
Для выполнения лабораторной работы был взят набор данных AG для классификации новосных тем.

Набор данных для классификации новостных тем AG состоит из 4 крупнейших классов, выбранных из исходного корпуса. Каждый класс содержит 30 000 обучающих и 1900 тестовых примеров. Общее количество обучающих примеров составляет 120 000, а тестовых — 7600.

индекс класса:
Состоит из 1–4 чисел, обозначающих класс: 1 — мир, 2 — спорт, 3 — бизнес, 4 — наука/технологии

Файлы train.csv и test.csv содержат все обучающие выборки в виде значений, разделённых запятыми. В них есть 3 столбца, соответствующие индексу класса (от 1 до 4), заголовку и описанию. Заголовок и описание заключены в двойные кавычки ("), а любая внутренняя двойная кавычка заключена в 2 двойные кавычки (""). Новые строки заключены в обратную косую черту, за которой следует символ "n", то есть "\n".

## модель 
целевой моделью была выбрана модель "distilbert-base-uncased" — облегчённый BERT (6 слоёв, hidden size 768), загружается через AutoModelForSequenceClassification с num_labels=4

## обучение 
для обучения мы разбиваем данные на 90(train)/10(test) обучающий и тестовые соответсвенно

При обучении целевой модели на всем обучающем датасете мы получили следующие результаты:

accuracy: 0.9495 

f1_macro: 0.9494756442515797}

далее случайным образом выбираем 1%, 10%, 20% данных из обучающего датасета и проводим обучение целевой модели на данной выборке 
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fraction</th>
      <th>seed</th>
      <th>num_samples</th>
      <th>f1_macro</th>
      <th>accuracy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.01</td>
      <td>13</td>
      <td>541</td>
      <td>0.864167</td>
      <td>0.864905</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.01</td>
      <td>21</td>
      <td>541</td>
      <td>0.862512</td>
      <td>0.863908</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.01</td>
      <td>34</td>
      <td>541</td>
      <td>0.821918</td>
      <td>0.827684</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.01</td>
      <td>55</td>
      <td>541</td>
      <td>0.855107</td>
      <td>0.857262</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.01</td>
      <td>89</td>
      <td>541</td>
      <td>0.858842</td>
      <td>0.860086</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.10</td>
      <td>13</td>
      <td>5415</td>
      <td>0.907511</td>
      <td>0.907611</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.10</td>
      <td>21</td>
      <td>5415</td>
      <td>0.908680</td>
      <td>0.908940</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.10</td>
      <td>34</td>
      <td>5415</td>
      <td>0.895739</td>
      <td>0.896311</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.10</td>
      <td>55</td>
      <td>5415</td>
      <td>0.899177</td>
      <td>0.899801</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.10</td>
      <td>89</td>
      <td>5415</td>
      <td>0.906473</td>
      <td>0.906613</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.20</td>
      <td>13</td>
      <td>10830</td>
      <td>0.917671</td>
      <td>0.917913</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.20</td>
      <td>21</td>
      <td>10830</td>
      <td>0.919041</td>
      <td>0.919242</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.20</td>
      <td>34</td>
      <td>10830</td>
      <td>0.918522</td>
      <td>0.918578</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.20</td>
      <td>55</td>
      <td>10830</td>
      <td>0.918463</td>
      <td>0.918578</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.20</td>
      <td>89</td>
      <td>10830</td>
      <td>0.918014</td>
      <td>0.918245</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-df4a24f6-a208-4e5b-b653-f8f92df9cd16')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

<div id="df-796b67d6-c6f7-44cf-b990-006de1fa5070" class="colab-df-container">
    <div>


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fraction</th>
      <th>mean_f1</th>
      <th>std_f1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.01</td>
      <td>0.852509</td>
      <td>0.017454</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.10</td>
      <td>0.903516</td>
      <td>0.005716</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.20</td>
      <td>0.918342</td>
      <td>0.000523</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-796b67d6-c6f7-44cf-b990-006de1fa5070')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>



