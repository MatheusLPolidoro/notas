---
sticker: lucide//album
---
# Programação Orientada a Objetos



```mehrmaid
flowchart LR
A --> B & C --> D --> E --> F & G
G --> F
A["![[logo.png|100]]"]
B("![[logo-old.png|100]]")
C("[[thisisalink]]")
D("$f(x)=\sum_i^\inf x^i$")
E("**Caption**
1. **Bold**
2. *Italic*
3. ==Marker==
- [ ] Point
---
Different Section")
F("#uni")
G(("$\dfrac{2}{\pi}+2$"))
```


```python
class MinhaClasse:

	def __init__(self, info, elemento): # metodo construtor
		self.atributo_1 = 'meu atributo'
		self.atributo_2 = [1, 2, 'a']
		self.atributo_3 = elemento
		self.atributo_novo = info
		print(self.atributo_novo)

	def metodo_1(self):
		print('minha ação 1')
		print('minha ação 2')
		return 'olá mundo!'

	def metodo_2(self, numero):
		self.metodo_1()
		print(self.atributo_2[1] + numero)

# objeto       # classe -> instanciamos um objeto
minha_classe = MinhaClasse()

minha_classe.metodo_2(3)
```
