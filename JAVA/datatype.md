# ์๋ฃํ ๐

## ์ข๋ฅ
- ๊ธฐ๋ณธ ์๋ฃํ
- ์ฐธ์กฐ ์๋ฃํ

---

## ๐๊ธฐ๋ณธ ์๋ฃํ 
๊ธฐ๋ณธ ์๋ฃํ์ ์๋ฐ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์์ ๊ธฐ๋ณธ์ผ๋ก ์ ๊ณตํ๋ฉฐ, ์ผ๋ง๋งํผ์ ๋ฉ๋ชจ๋ฆฌ๋ฅผ ์ด๋ป๊ฒ ์ฌ์ฉํ  ๊ฒ์ธ์ง๊ฐ ์ด๋ฏธ ์ ํด์ ธ ์์ต๋๋ค.

### ๊ธฐ๋ณธ ์๋ฃํ์ ์ข๋ฅ
- ์ ์ํ
- ๋ฌธ์ํ
- ์ค์ํ
- ๋ผ๋ฆฌํ

---

### ๐ข์ ์ํ
์ ์ ์๋ฃํ์ ์์, ์์, 0์ ๋ํ๋ด๋ ๋ฐ ์ฌ์ฉํ๋ ์๋ฃํ ์๋๋ค.
- byte ( 1๋ฐ์ดํธ )
- short ( 2๋ฐ์ดํธ )
- int ( 4๋ฐ์ดํธ ) -> ๊ธฐ๋ณธ
- long ( 8๋ฐ์ดํธ )

โญ ์๋ฐ๋ ๋ชจ๋  ์ ์ ๊ฐ์ ๊ธฐ๋ณธ int ํ์ผ๋ก ์ฒ๋ฆฌํฉ๋๋ค.  
 int์ ๋ฒ์๋ฅผ ๋์ ์ซ์๋ฅผ ์ฒ๋ฆฌํ๊ณ  ์ถ์ผ๋ฉด longํ์ ์ฌ์ฉํด์ผ ํฉ๋๋ค.   
 ๊ทธ๋ฌ๊ธฐ ์ํด์๋ longํ์ ๋ํ๋ด๋ ์๋ณ์์ธ L์ด๋ l์ ์ซ์ ๋ค์ ๋ถ์ฌ์ผ ํฉ๋๋ค. โญ  
`ex ) long num = 12345678900L;`


### ๐ก๋ฌธ์ํ
์ปดํจํฐ๋ 0๊ณผ 1๋ก๋ง ํํํ  ์ ์์ผ๋ฏ๋ก ๋ฌธ์๋ฅผ ๋ณ์์ ๋์ํ๋ฉด ๋ฌธ์ ๊ทธ๋๋ก ์ ์ฅ๋๋ ๊ฒ์ด ์๋๋ผ ๊ทธ ๋ฌธ์์ ํด๋นํ๋ ์ ์ ๊ฐ( ์์คํค ์ฝ๋ ๊ฐ ) ์ด ์ ์ฅ๋ฉ๋๋ค.
- char ( 2๋ฐ์ดํธ )

๋ฌธ์๋ฅผ ์ฌ์ฉํ  ๋๋ ํญ์ `์์๋ฐ์ดํ( ' ' )`๋ฅผ ์ฌ์ฉํ๊ณ , ๋ฌธ์์ด์ ์ฌ์ฉํ  ๋๋ `ํฐ๋ฐ์ดํ( " " )`๋ฅผ ์ฌ์ฉํฉ๋๋ค.  

โญ์๋ฐ์์ ๋ฌธ์์ด์ ๋ค๋ฃฐ๋๋ Stringํด๋์ค๋ฅผ ์ฌ์ฉํฉ๋๋ค. ( char ์ฌ์ฉ xx )โญ

### ๐ข์ค์ํ
- float ( 4๋ฐ์ดํธ )
- double ( 8๋ฐ์ดํธ ) -> ๊ธฐ๋ณธ

โญ ์๋ฐ์์ ์ค์๋ doubleํ์ ๊ธฐ๋ณธ์ผ๋ก ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ floatํ์ ์ฌ์ฉํ  ๋์๋ floatํ์ ๋ํ๋ด๋ ์๋ณ์์ธ F๋ f๋ฅผ ์ซ์ ๋ค์ ๋ถ์ฌ์ฃผ์ด์ผ ํฉ๋๋ค. โญ
`ex ) float height = 155.5F;`


### โญ๋ผ๋ฆฌํโ
์ด๋ค ๋ณ์์ ์ฐธ, ๊ฑฐ์ง์ ๊ฐ์ ๋ํ๋ด๋ ๋ฐ ์ฌ์ฉํฉ๋๋ค. 
- boolean ( 1๋ฐ์ดํธ )
    - true ( ์ฐธ )
    - false ( ๊ฑฐ์ง )
