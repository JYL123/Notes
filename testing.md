Mark directory as `Test resource root`

Test exception works 

@Test(expected = IllegalStateException.class)

Addressing dependencies with test doubles: 
code calls out to an external web service-> use test stub, not using the actual implementation 
polymorphism and dependency injection 

Mockito
don't require the creation of stub class
import static org.mockito.Mockito.*
IinterfaceClass mockClass = mock(IinterfaceClass.class)
when(mockClass.funtion("xxx"/any())).thenReturn("yyy")
assertTrue()
assertFalse()

[doReturn vs. thenReturn](https://stackoverflow.com/questions/20353846/mockito-difference-between-doreturn-and-when)
CTRL+SHIFT+T shortcut on intelliJ to create test classes
