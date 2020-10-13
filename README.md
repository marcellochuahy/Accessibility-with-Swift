# Accessibility-with-Swift


```
import Foundation

let formattedCpf = "524.265.600-02"
let formattedCnpj = "63.620.430/0001-26"

func accessibilityLabelFor(formattedCpfOrCnpj cpfOrCnpj: String) -> String {
	
	let pauseCharacter = "…" // Option + semicolon
	
	var accessibilityValue: String
	accessibilityValue = cpfOrCnpj.map{String($0)}.joined(separator: " ")
	accessibilityValue = accessibilityValue.replacingOccurrences(of: ".", with: pauseCharacter)
	accessibilityValue = accessibilityValue.replacingOccurrences(of: "/", with: pauseCharacter + " barra " + pauseCharacter)
	accessibilityValue = accessibilityValue.replacingOccurrences(of: "-", with: pauseCharacter + " dígito " + pauseCharacter)
	
	return accessibilityValue
	
}

let accessibilityLabelForFormattedCpf = accessibilityLabelFor(formattedCpfOrCnpj: formattedCpf)
let accessibilityLabelForFormattedCnpj = accessibilityLabelFor(formattedCpfOrCnpj: formattedCnpj)

print(accessibilityLabelForFormattedCpf) // 5 2 4 … 2 6 5 … 6 0 0 … dígito … 0 2
print(accessibilityLabelForFormattedCnpj) // 6 3 … 6 2 0 … 4 3 0 … barra … 0 0 0 1 … dígito … 2 6
```
