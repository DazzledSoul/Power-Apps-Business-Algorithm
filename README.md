# Power-Apps-Helper

**Contextual variable:**

UpdateContext({var:Card.Text,var2:Card2.Selected.Value})


**Global Variable:**

Set(var,Card.Text);Set(var2,Card2.Text)


**Patch Function:**

-To Update: Patch(List,Gallery.Selected,{'Col':"Value",'Col2':"Value2"})

-To Add: Patch(List,Defaults(List),{'Col':"Value",'Col2':"Value2"})

**Login Validation:**

-Button >> OnSelect >> if(!IsBlank(Lookup(List,Username=Input1.Text,password=Input2.Text).Username),Navigate(Success),UpdateContext({showErrorMessage: true}))

-TextLabel >> Visible >> showErrorMessage

**Cascading Form:**
-DropDown1 >> item >> Distinct(List,Column1)

-DropDown2 >> item >> Filter(List,Column1 = Card.Selected.Value).Column2

**Data Validation:**
-BorderColor >> If(IsBlank(ErrorMessage.Text), Parent.BorderColor, Color.Red)

-ErrorMessage >> Coalesce(
    Parent.Error,
    If(
        !IsBlank(DataCard.Text) && Len(DataCard.Text) <> 10,
        "Enter 10 Digits"
    ),
    If(
        !IsBlank(DataCard.Text) && !IsMatch(DataCard.Text,Match.MultipleDigits),
        "Enter Digits only"
    )
    If(
        !IsBlank(DataCard.Text) && Value(DataCard.Text)>10,
        "Enter Value less than 10"
    )
)
-required >> true

**CRUD:**
-Form1 >> Item >> Gallery.Selected
-Button1 >> NewForm(Form1)
-Button2 >> SubmitForm(Form1)
-Button3 >> ResetForm(Form1)
-Button4 >> EditForm(Form1)
-Button5(in gallery) >> Remove(List,ThisItem)

**Autofill:**
-DropDown >> item >> Distinct(List,Col1)
-DropDown >> OnChange >> Set(var,Lookup(List,Col1=dropdown.Selected.Value))
-Card >> item >> var.Colname

**Search:**
Gallery >> item >> Search(List,Input1.Text,"Col1","Col2")

