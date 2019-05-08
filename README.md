# Adianti

Adianti framework fornece um conjunto de componentes (containers e widgets) para construir interfaces. Você pode construir a interface digitando ou usando o Studio Designer, criador de interfaces.

## QuickStart

**Configuração do banco de dados**

Todos os bancos de dados são configurados nos arquivos `.ini` que está em `app > config`

```
host   =  
name   = "app/database/sample.db" 
user   =  
pass   = 
type   = "sqlite"
```

O Banco de dados externos são adicionado na pasta `app > database`

**Model**

Os modelos (entidades) da apicação são salvos em `app > model`, a extenção das model são salvos usuando `.class.php`

Todas as model extendem de `TRecord`, essa classe possuí todos os metódos de perssistencia do banco de dados

```
class Exemplo extends TRecord
{
  const TABLENAME = 'nome-do-banco';
  const PRIMARYKEY = 'id';
  
  public function __construct($id = NULL)
  {
    parent::__construct($id);
    parent::addAttribute('field');
  }
}
```
Para adicionar os atributos no model deve-se usar o metódo `addAttribute('field')` da casse TRecord

**Control**

O control é utilizado para controlar as requisições e para gerar as views do adianti, os controls são salvos em `app > control`

Os controles pode extender de `TPage` ou `TWindow`
