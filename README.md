# Global design and architecture considerations and guides

## Balance and currency formatting

1. The balances or currencies will be separated by comma;
2. The balances or currencies will use a dot as a decimal separator;
3. The balances or currencies will show 2 decimal places.

> example: `10,395,415.96 cUSDC`

## About form inputs, input sliders, get max balances

Care must be taken in how to display user balances in forms.
For example, a user has a balance of `14,949.195312139837896916 cUSDC` if the decimal places to be used is 2 then it is better to display the balance as `14,949.19` and not round up and end up displaying `14,949.20`. So the value will be truncated first to two decimal before parsing it using the function below.

```
 new Intl.NumberFormat("en-US", {
    maximumFractionDigits: 2,
    minimumFractionDigits: 2,
  }).format(number);
```

With this we can not give the wrong idea to the users that their balance is greater that the actual value even if it is on the hundredths place.

Now, when the user clicks the <strong>Max</strong> button to easily get the maximum usable balance the input would display the real unparsed balance and that is `14,949.195312139837896916`. With this we can be more transparent. The same idea goes for the usage of the slider.

Note: this idea is inspired by the [Uniswap app swap UI](https://app.uniswap.org/).

**With max value.** <br />

![With Max value](https://res.cloudinary.com/vaughn-pictures/image/upload/v1651538461/f5b7986a-8d17-460b-83c7-4b1478075e06-Screen%20Shot%202022-05-03%20at%2008.40.31.png.png)

**With about 60% of the balance** <br/>
![With about 60% of the balance](https://res.cloudinary.com/vaughn-pictures/image/upload/v1651538624/4e9e8e26-49ad-46ea-8b7b-79bcc3796e10-Screen%20Shot%202022-05-03%20at%2008.40.38.png.png)
