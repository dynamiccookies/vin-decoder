# vin-decoder.php

![GitHub](https://img.shields.io/github/license/dynamiccookies/vin-decoder?style=for-the-badge)
![GitHub file size in bytes](https://img.shields.io/github/size/dynamiccookies/vin-decoder/vin-decoder.php?style=for-the-badge)
![GitHub Release Date](https://img.shields.io/github/release-date/dynamiccookies/vin-decoder?style=for-the-badge)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/dynamiccookies/vin-decoder?style=for-the-badge)

Use this function to get details about a vehicle from its VIN. 

The data is pulled from the [National Highway Traffic Safety Administration's (NHTSA) API](https://vpic.nhtsa.dot.gov/api/). 

## Installation
1. Download the vin-decoder.php file from the [latest releases page](https://github.com/dynamiccookies/vin-decoder/releases)
2. Upload the file to your website
3. Include the file in your code using `include_once 'vin-decoder.php';`
   - Ensure the decoder file is in the same directory as the file you call it from, or
   - Update the `include_once` path to the file 

## Calling the Function
Call the `decodeVIN()` function using one of the following three methods:

1. VIN only (returns entire array)
```
decodeVIN('4T1SK12E1NU028452');
```
2. Secondary parameter as an array using [splat](https://stackoverflow.com/questions/41124015/meaning-of-three-dot-in-php) (only returns values specified)
```
$options = array('Make','Model','ModelYear','Trim');
decodeVIN('4T1SK12E1NU028452', ...$options);
```
3. VIN as variable and additional parameters as strings (only returns values specified)
```
$vin = '4T1SK12E1NU028452';
decodeVIN($vin, 'Make','Model','ModelYear','Trim');
```

## Return Values
For Example #1, the complete array from the NHTSA API is returned with more 130+ attributes.

For Examples #2 and #3, the following array is returned:
```
Array ( [Error] => 0 [Make] => TOYOTA [Model] => Camry [ModelYear] => 1992 [Trim] => )
```

In the event of an invalid VIN being submitted, an array with the keys `['Error']` and `[Searched]'` is returned. 
 - The `['Error']` key holds an array of error messages.
 - The `['Searched']` key returns the value that was searched so that you may check it for errors. 

So, when searching for an invalid VIN like `4T1SK12E00U028452` (notice the 9th & 10th digits), the following array is returned:
```
Array ( 
  [Error] => Array ( 
    [0] => 11 - Incorrect Model Year - Position 10 does not match valid model year codes (I, O, Q, U, Z, 0). Decoded data may not be accurate. 
    [1] => 400 - Invalid Characters Present 
  ) 
  [Searched] => VIN(s): 4T1SK12E00U028452 
)
```


## License

This project uses the following license: [MIT](LICENSE).
