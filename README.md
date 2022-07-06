# Java.calculator
 
const digits = {
    Z: 2000,
    M: 1000,
    CM: 900,
    D: 500,
    CD: 400,
    C: 100,
    XC: 90,
    L: 50,
    XL: 40,
    X: 10,
    IX: 9,
    VIII:8,
    VII:7,
    VI:6,
    V: 5,
    IV: 4,
    III:3,
    II: 2,
    I: 1

}

    const stringValidation = string => {
    let pattern = /[^IVX0-9+*\/-\s]/g
    if([...string.matchAll(pattern)].length >= 1) {
        throw new Error("В строке обнаружены неккоректные символы")
        }
    
    pattern = /[+*\/-]{2,}/g
    if([...string.matchAll(pattern)].lenth >=1) {
        throw new Error("Строка указана неккоректно, в строке более 1 операнда для вычесления")
        }
        return true
    }
    
    const getOperation = string => {
        return [...string.match(/[+*\/-]{2,}/g)][0]
    }

    const getNums = string => {
       return string.split(/[+*\/-]/g).map(num => num.trim())
    }
    const romanToArrabic = string => {
        return string.split('').reduce((prevVAl, currValue, i, arr) => {
            debugger
            const [a, b, c] = [
            digits[arr[i]],
            digits[arr[i + 1]],
            digits[arr[i + 2]]
            ]
            return b > a ? prevVal - a : prevVal + a
    }, 0)
    }

    const isRoman = string => {
        const pattern = /^[IVX]+$/
        let arrNums = string.split(/[+*\/-]{2,}/g).map(num.trim())
        const countRoman = arrNums.reduce((prevVAl, currValue) => prevVal + pattern.test(currValue), 0)
        if(countRoman === 1) {
            throw new Error("Оба числа должны быть римскими либо арабскими")
        } else if (countRoman === 2) {
        return true 
        }
    } 

    const sum = nums => {
        return nums.reduce((a, b) => a + b)
    }

    const mult = nums => {
        return nums.reduce((a, b) => a * b)
    }
    const division = nums => {
        return nums.reduce((a, b) => a / b)
    }
    const substraction = nums => {
        return nums.reduce((a, b) => a - b)
    }

    const checkOperation = (str, nums) => {
        let result;
        if (str === '+') {
            sum(nums)
        } else if (str === '*') {
            mult(nums)
        } else if (str === '/') {
            division(nums)
        } else if (str === '-') {
            subtraction(nums)
        }
        return Math.floor(result)
    }

     const calculator = string => {
        const isValid = stringValidation(string)
        const operation = getOperation(string)
        let nums = getNums(string)
        const roman = isRoman(string)
        if(roman) {
            nums = nums.map(num => romanToArrabic(num))
        }
        nums = nums.map(num => +num)
        return checkOperation(operation, nums)
     }

    console.log(calculator("X + III"))
    console.log(calculator("10 + 5")) 
    
