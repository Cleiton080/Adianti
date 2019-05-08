# Adianti

Adianti framework fornece um conjunto de componentes (containers e widgets) para construir interfaces. Você pode construir a interface digitando ou usando o Studio Designer, criador de interfaces.

## QuickStart

### Configuração do banco de dados

Todos os bancos de dados são configurados nos arquivos `.ini` que está em `app > config`

```
host   =  
name   = "app/database/sample.db" 
user   =  
pass   = 
type   = "sqlite"
```

O Banco de dados externos são adicionado na pasta `app > database`

### Model

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

### Control

O control é utilizado para controlar as requisições e para gerar as views do adianti, os controls são salvos em `app > control`. Os controles pode extender de `TPage` ou `TWindow`, o TPage é uma página comum, enquanto um TWindow é uma página em formato de janela.

## Elementos do Adianti

### Formulários

#### Label

Use um objeto `TLabel` para instânciar uma label, no construtor deve ser passado o nome da label.

```
$myLabel = new TLabel('nome-label');
```

#### Inputs

Para criar inputs no adianti deve-se utilizar o objeto `TEntry`, no construtor pode ser passado o name do input.

```
$myInput = new TEntry('name');
```

##### Mascáras dos Inputs

As máscaras são definidas através do metódo dos Inputs `->setMask('')`, o parâmetro informado no construtor é a representação da mascára.

```
$myInput->setMask('(71)99999-9999');
```

#### Formulários Rápidos

Para a criação de formulários sem muitas formatações deve ser utilizado o objeto `TQuickForm`, lembrando de passar o nome que representa o formulário como parâmetro no construtor do objeto.

```
$myForm = new TQuickForm('name-form');
```
##### Adicionar os Inputs no Formulário

O método `->addQuickField()` é utilizado para adicionar os labels e inputs criados no formulário.

```
$myForm->addQuickField($myLabel, $myInput);
```

##### Botões com ações 

O método `->addQuickAction()` adiciona um botão com uma ação para o mesmo, veja o exemplo:

```
$myForm->addQuickAction('nome-botao', $action, [icon]);

```

As ações são representadas com o objeto `TAction`, em seu construtor deve ser passado o método que irá ser executado quando o botão for clicado.

```
$action = new TAction(array($this, 'onSave');
```

Ou seja, a representação do método `->addQuickAction()` ficará da seguinte forma:

```
$myForm->addQuickAction('Save', new TAction(array($this, 'onSave')));
```

Agora deve-se criar o método especificado no construtor do Action, no nosso caso utilizamos o `onSave`.

```
public function onSave()
{
  // Quando o botão for clicado esse método será executado
}
```

Agora só está faltando adicionar o formulario na página, para ser utilizado.

```
parent::add($myForm);
```

Veja o examplo completo dos componentes que vimos até aqui:

```
class Exemplo extends TPage
{
    protected $form;

    public function __construct()
    {
        parent::__construct();

        $this->form = new TQuickForm('form');

        $cpfField = new TEntry('cpf');
        $nameField = new TEntry('name');
        $birthdayField = new TEntry('birthday');

        $nameLabel = new TLabel('Name: ');
        $cpfLabel = new TLabel('CPF: ');
        $birthdayLabel = new TLabel('Birthday: ');

        $cpfField->setMask('999.999.999-99');
        $birthdayField->setMask('99/99/9999');

        $this->form->addQuickField($nameLabel, $nameField);
        $this->form->addQuickField($cpfLabel, $cpfField);
        $this->form->addQuickField($birthdayLabel, $birthdayField);
        $this->form->addQuickAction ('Save', new TAction(array($this, 'onSave')));
        
        parent::add($myForm);
    }
    
    public function onSave()
    {
      // Quando o botão for clicado esse método será executado
    }
```
