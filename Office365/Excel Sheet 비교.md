# Excel Sheet 비교

새로운 시트를 만들고 아래와 같은 수식을 쓴다.

> =IF('Sheet1'!A1 <> 'Sheet12'!A1, "Sheet1:"&'Sheet1'!A1&" vs Sheet2:"&'Sheet2'!A1, "")

채우기를 통해 확장한다.