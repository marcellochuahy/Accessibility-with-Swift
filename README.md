# Accessibility-with-Swift


```
import Foundation

let formattedCpf     = "524.265.600-02"
let formattedCnpj    = "63.620.430/0001-26"
let fullMobileNumber = "+55 11 98765-4321"
let randomKey        = "AdFet-A"

// --------------------------------------------

func accessibilityLabelFor(formattedCpfOrCnpj cpfOrCnpj: String) -> String {
	
	let pauseCharacter = "…" // Option + semicolon
	
	var accessibilityValue: String
	accessibilityValue = cpfOrCnpj.map{String($0)}.joined(separator: " ")
	accessibilityValue = accessibilityValue.replacingOccurrences(of: ".", with: pauseCharacter)
	accessibilityValue = accessibilityValue.replacingOccurrences(of: "/", with: pauseCharacter + " barra " + pauseCharacter)
	accessibilityValue = accessibilityValue.replacingOccurrences(of: "-", with: pauseCharacter + " dígito " + pauseCharacter)
	
	return accessibilityValue
	
}

func accessibilityLabelFor(fullMobileNumber: String) -> String {
	
	let pauseCharacter = " … " // Option + semicolon
	
	var accessibilityValue: String
	
	let components   = fullMobileNumber.components(separatedBy: " ")
	let prefix       = components[0]
	let ddd          = components[1]
	let mobileNumber = components[2]

	let firstBlockOfDigitsOfMobileNumber = mobileNumber.prefix(1)
	
	let startOfSecondBlockOfDigitsOfMobileNumber       = mobileNumber.index(mobileNumber.startIndex, offsetBy: 1)
	let endOfSecondBlockOfDigitsOfMobileNumber         = mobileNumber.index(mobileNumber.startIndex, offsetBy: 5)
	let rangeOfSecondBlockOfDigitsOfMobileNumber       = startOfSecondBlockOfDigitsOfMobileNumber..<endOfSecondBlockOfDigitsOfMobileNumber
	let secondBlockOfDigitsOfMobileNumber              = mobileNumber[rangeOfSecondBlockOfDigitsOfMobileNumber]
	let accessibilitySecondBlockOfDigitsOfMobileNumber = secondBlockOfDigitsOfMobileNumber.map{String($0)}.joined(separator: " ")
	
	let startOfThirdBlockOfDigitsOfMobileNumber       = mobileNumber.index(mobileNumber.startIndex, offsetBy: 6)
	let endOfThirdBlockOfDigitsOfMobileNumber         = mobileNumber.index(mobileNumber.endIndex, offsetBy: 0)
	let rangeOfThirdBlockOfDigitsOfMobileNumber       = startOfThirdBlockOfDigitsOfMobileNumber..<endOfThirdBlockOfDigitsOfMobileNumber
	let thirdBlockOfDigitsOfMobileNumber              = mobileNumber[rangeOfThirdBlockOfDigitsOfMobileNumber]
	let accessibilityThirdBlockOfDigitsOfMobileNumber = thirdBlockOfDigitsOfMobileNumber.map{String($0)}.joined(separator: " ")
	
	accessibilityValue  = prefix
	accessibilityValue += pauseCharacter + ddd
	accessibilityValue += pauseCharacter + firstBlockOfDigitsOfMobileNumber
	accessibilityValue += pauseCharacter + accessibilitySecondBlockOfDigitsOfMobileNumber
	accessibilityValue += pauseCharacter + accessibilityThirdBlockOfDigitsOfMobileNumber
	
	return accessibilityValue
	
}

func accessibilityLabelFor(randomKey: String) -> String {
	return randomKey.map{String($0)}.joined(separator: " ")
}

// --------------------------------------------

let accessibilityLabelForFormattedCpf          = accessibilityLabelFor(formattedCpfOrCnpj: formattedCpf)
let accessibilityLabelForFormattedCnpj         = accessibilityLabelFor(formattedCpfOrCnpj: formattedCnpj)
let accessibilityLabelForFormattedMobileNumber = accessibilityLabelFor(fullMobileNumber: fullMobileNumber)
let accessibilityLabelForRandomKey             = accessibilityLabelFor(randomKey: randomKey)

print(accessibilityLabelForFormattedCpf)          // 5 2 4 … 2 6 5 … 6 0 0 … dígito … 0 2
print(accessibilityLabelForFormattedCnpj)         // 6 3 … 6 2 0 … 4 3 0 … barra … 0 0 0 1 … dígito … 2 6
print(accessibilityLabelForFormattedMobileNumber) // +55 … 11 … 9 … 8 7 6 5 … 4 3 2 1
print(accessibilityLabelForRandomKey)             // A d F e t - A
```
