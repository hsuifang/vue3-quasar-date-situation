# Using Date and DateRange with Quasar

透過 Vue3 及 Quasar 的 Date 與 DatePicker 去實作以下操作情境：選擇單一日期、兩個 Input 框選擇起迄日期及一次選擇區間，並在三種情境下，條列部分限制，如：選擇時間的長度、開始日小於結束日期等。

首先先製作預期元件:

## 元件製作

點擊輸入框的 Icon，顯示選擇日期的元件
![輸入框](https://i.imgur.com/aOlsFHc.png)
![點擊呈現](https://i.imgur.com/S0Ib6HL.png)

```
<q-input
  dense
  filled
  v-model="second.start"
  mask="####-##-##"
  :rules="[v => !Number.isNaN(new Date(v).valueOf())]"
>
  <template v-slot:append>
    <q-icon name="event" class="cursor-pointer">
      <q-popup-proxy
        transition-show="scale"
        transition-hide="scale"
      >
        <q-date
          v-model="second.start"
          mask="YYYY-MM-DD"
          :options="secondStart"
          today-btn
        >
          <div class="row items-center justify-end">
            <q-btn
              v-close-popup
              label="Close"
              color="primary"
              flat
            />
          </div>
        </q-date>
      </q-popup-proxy>
    </q-icon>
  </template>
</q-input>

```

## Date 情境實現

> 透過 mask 設定日期呈現方式
> 透過 rule 檢查日期合法與否

### Date - 選擇單一日期

限制：
- 搭配 input 框去顯示

- 時間限制：選擇小於等於今天

```
beforeToday(date) {
  return new Date(date) <= new Date()
},
```

### Date - 選擇起訖

- 搭配 input 框去顯示
- 時間限制：開始日 <= 結束日
- 選擇區間限制 xx 天

### DateRange
