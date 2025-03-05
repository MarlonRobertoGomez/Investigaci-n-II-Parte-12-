Template Method
using System;

public abstract class Bebida
{
    // Este es el Template Method
    public void PrepararBebida()
    {
        HervirAgua();
        PrepararIngrediente();
        VerterEnTaza();
        AgregarExtras();
    }

    // Paso común
    private void HervirAgua()
    {
        Console.WriteLine("Hirviendo agua...");
    }

    // Paso que debe ser implementado por las subclases
    protected abstract void PrepararIngrediente();

    // Paso común
    private void VerterEnTaza()
    {
        Console.WriteLine("Vertiendo en la taza...");
    }

    // Paso opcional para agregar extras (puede ser sobrecargado si es necesario)
    protected virtual void AgregarExtras()
    {
        Console.WriteLine("No se agregan extras.");
    }
}

public class Te : Bebida
{
    protected override void PrepararIngrediente()
    {
        Console.WriteLine("Poniendo la bolsa de té en la taza.");
    }

    protected override void AgregarExtras()
    {
        Console.WriteLine("Agregando limón al té.");
    }
}

public class Cafe : Bebida
{
    protected override void PrepararIngrediente()
    {
        Console.WriteLine("Poniendo el café molido en la taza.");
    }

    protected override void AgregarExtras()
    {
        Console.WriteLine("Agregando azúcar al café.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Preparando Té:");
        Bebida te = new Te();
        te.PrepararBebida();

        Console.WriteLine("\nPreparando Café:");
        Bebida cafe = new Cafe();
        cafe.PrepararBebida();
    }
}

Visitor
public interface IVisitor
{
    void Visit(ElementoA elementoA);
    void Visit(ElementoB elementoB);
}
public abstract class Elemento
{
    public abstract void Aceptar(IVisitor visitor);
}

public class ElementoA : Elemento
{
    public string Nombre { get; set; }

    public override void Aceptar(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}

public class ElementoB : Elemento
{
    public int Valor { get; set; }

    public override void Aceptar(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}
public class VisitorConcreto : IVisitor
{
    public void Visit(ElementoA elementoA)
    {
        Console.WriteLine($"Visitando ElementoA: {elementoA.Nombre}");
    }

    public void Visit(ElementoB elementoB)
    {
        Console.WriteLine($"Visitando ElementoB: {elementoB.Valor}");
    }
}
class Program
{
    static void Main(string[] args)
    {
        List<Elemento> elementos = new List<Elemento>
        {
            new ElementoA { Nombre = "Elemento A 1" },
            new ElementoB { Valor = 100 },
            new ElementoA { Nombre = "Elemento A 2" }
        };

        IVisitor visitor = new VisitorConcreto();

        // Aplicar el visitor a cada elemento
        foreach (var elemento in elementos)
        {
            elemento.Aceptar(visitor);
        }
    }
}
Visitando ElementoA: Elemento A 1
Visitando ElementoB: 100
Visitando ElementoA: Elemento A 2

