---
title: Alternativa de DataContract
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0188f3c-00a9-4cf0-a887-a2284c8fb014
caps.latest.revision: "21"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: 77eee3172b24bc0252ecb18d9ce6b283ba6e5c93
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="datacontract-surrogate"></a><span data-ttu-id="24095-102">Alternativa de DataContract</span><span class="sxs-lookup"><span data-stu-id="24095-102">DataContract Surrogate</span></span>
<span data-ttu-id="24095-103">Este exemplo demonstra como processos como a serialização, desserialização, exportação de esquema e importação de esquema podem ser personalizados usando um contrato de dados alternativos classe.</span><span class="sxs-lookup"><span data-stu-id="24095-103">This sample demonstrates how processes like serialization, deserialization, schema export, and schema import can be customized using a data contract surrogate class.</span></span> <span data-ttu-id="24095-104">Este exemplo mostra como usar um substituto em um cenário de cliente e servidor onde os dados são serializados e transmitidos entre um [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] cliente e serviço.</span><span class="sxs-lookup"><span data-stu-id="24095-104">This sample shows how to use a surrogate in a client and server scenario where data is serialized and transmitted between a [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] client and service.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="24095-105">As instruções de procedimento e a compilação de configuração para este exemplo estão localizadas no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="24095-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="24095-106">O exemplo usa o contrato de serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="24095-106">The sample uses the following service contract:</span></span>  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
[AllowNonSerializableTypes]  
public interface IPersonnelDataService  
{  
    [OperationContract]  
    void AddEmployee(Employee employee);  
  
    [OperationContract]  
    Employee GetEmployee(string name);  
}  
```  
  
 <span data-ttu-id="24095-107">O `AddEmployee` operação permite que os usuários adicionem dados sobre os novos funcionários e `GetEmployee` operação oferece suporte a pesquisa para funcionários com base no nome.</span><span class="sxs-lookup"><span data-stu-id="24095-107">The `AddEmployee` operation allows users to add data about new employees and the `GetEmployee` operation supports search for employees based on name.</span></span>  
  
 <span data-ttu-id="24095-108">Essas operações usam o tipo de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="24095-108">These operations use the following data type:</span></span>  
  
```  
[DataContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
class Employee  
{  
    [DataMember]  
    public DateTime dateHired;  
  
    [DataMember]  
    public Decimal salary;  
  
    [DataMember]  
    public Person person;  
}  
```  
  
 <span data-ttu-id="24095-109">No `Employee` tipo, o `Person` (mostrado no código de exemplo a seguir) de classe não pode ser serializado pelo <xref:System.Runtime.Serialization.DataContractSerializer> porque ele não é uma classe de contrato de dados válido.</span><span class="sxs-lookup"><span data-stu-id="24095-109">In the `Employee` type, the `Person` class (shown in the following sample code) cannot be serialized by the <xref:System.Runtime.Serialization.DataContractSerializer> because it is not a valid data contract class.</span></span>  
  
```  
public class Person  
{  
    public string firstName;  
  
    public string lastName;  
  
    public int age;  
  
    public Person() { }  
}  
```  
  
 <span data-ttu-id="24095-110">Você pode aplicar o `DataContract` de atributo para o `Person` classe, mas isso nem sempre é possível.</span><span class="sxs-lookup"><span data-stu-id="24095-110">You can apply the `DataContract` attribute to the `Person` class, but this is not always possible.</span></span> <span data-ttu-id="24095-111">Por exemplo, a `Person` classe pode ser definida em um assembly separado durante o qual você não tem controle.</span><span class="sxs-lookup"><span data-stu-id="24095-111">For example, the `Person` class can be defined in a separate assembly over which you have no control.</span></span>  
  
 <span data-ttu-id="24095-112">Dada essa restrição, uma maneira para serializar o `Person` classe é para substituí-lo por outra classe que é marcado com `DataContractAttribute` e copie os dados necessários para a nova classe.</span><span class="sxs-lookup"><span data-stu-id="24095-112">Given this restriction, one way to serialize the `Person` class is to substitute it with another class that is marked with `DataContractAttribute` and copy over necessary data to the new class.</span></span> <span data-ttu-id="24095-113">O objetivo é fazer o `Person` classe aparecem como DataContract para o <xref:System.Runtime.Serialization.DataContractSerializer>.</span><span class="sxs-lookup"><span data-stu-id="24095-113">The objective is to make the `Person` class appear as a DataContract to the <xref:System.Runtime.Serialization.DataContractSerializer>.</span></span> <span data-ttu-id="24095-114">Observe que essa é uma maneira para serializar as classes de contrato de dados não.</span><span class="sxs-lookup"><span data-stu-id="24095-114">Note that this is one way to serialize non-data contract classes.</span></span>  
  
 <span data-ttu-id="24095-115">O exemplo logicamente substitui o `Person` classe com uma classe diferente chamada `PersonSurrogated`.</span><span class="sxs-lookup"><span data-stu-id="24095-115">The sample logically replaces the `Person` class with a different class named `PersonSurrogated`.</span></span>  
  
```  
[DataContract(Name="Person", Namespace = "http://Microsoft.ServiceModel.Samples")]  
public class PersonSurrogated  
{  
    [DataMember]  
    public string FirstName;  
  
    [DataMember]  
    public string LastName;  
  
    [DataMember]  
    public int Age;  
}  
```  
  
 <span data-ttu-id="24095-116">O substituto de contrato de dados é usado para atingir essa substituição.</span><span class="sxs-lookup"><span data-stu-id="24095-116">The data contract surrogate is used to achieve this replacement.</span></span> <span data-ttu-id="24095-117">Um substituto de contrato de dados é uma classe que implementa <xref:System.Runtime.Serialization.IDataContractSurrogate>.</span><span class="sxs-lookup"><span data-stu-id="24095-117">A data contract surrogate is a class that implements <xref:System.Runtime.Serialization.IDataContractSurrogate>.</span></span> <span data-ttu-id="24095-118">Neste exemplo, a `AllowNonSerializableTypesSurrogate` classe implementa essa interface.</span><span class="sxs-lookup"><span data-stu-id="24095-118">In this sample, the `AllowNonSerializableTypesSurrogate` class implements this interface.</span></span>  
  
 <span data-ttu-id="24095-119">Na implementação de interface, a primeira tarefa é estabelecer um mapeamento de tipo de `Person` para `PersonSurrogated`.</span><span class="sxs-lookup"><span data-stu-id="24095-119">In the interface implementation, the first task is to establish a type mapping from `Person` to `PersonSurrogated`.</span></span> <span data-ttu-id="24095-120">Isso é usado tanto em tempo de serialização, bem como em tempo de exportação de esquema.</span><span class="sxs-lookup"><span data-stu-id="24095-120">This is used both at serialization time as well as at schema export time.</span></span> <span data-ttu-id="24095-121">Esse mapeamento é obtido com a implementação de <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%28System.Type%29> método.</span><span class="sxs-lookup"><span data-stu-id="24095-121">This mapping is achieved by implementing the <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%28System.Type%29> method.</span></span>  
  
```  
public Type GetDataContractType(Type type)  
{  
    if (typeof(Person).IsAssignableFrom(type))  
    {  
        return typeof(PersonSurrogated);  
    }  
    return type;  
}  
```  
  
 <span data-ttu-id="24095-122">O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%28System.Object%2CSystem.Type%29> método mapeia um `Person` de instância para um `PersonSurrogated` instância durante a serialização, conforme mostrado no código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="24095-122">The <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%28System.Object%2CSystem.Type%29> method maps a `Person` instance to a `PersonSurrogated` instance during serialization, as shown in the following sample code.</span></span>  
  
```  
public object GetObjectToSerialize(object obj, Type targetType)  
{  
    if (obj is Person)  
    {  
        Person person = (Person)obj;  
        PersonSurrogated personSurrogated = new PersonSurrogated();  
        personSurrogated.FirstName = person.firstName;  
        personSurrogated.LastName = person.lastName;  
        personSurrogated.Age = person.age;  
        return personSurrogated;  
    }  
    return obj;  
}  
```  
  
 <span data-ttu-id="24095-123">O <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%28System.Object%2CSystem.Type%29> método fornece o mapeamento inverso para desserialização, conforme mostrado no código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="24095-123">The <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%28System.Object%2CSystem.Type%29> method provides the reverse mapping for deserialization, as shown in the following sample code.</span></span>  
  
```  
public object GetDeserializedObject(object obj,   
Type targetType)  
{  
    if (obj is PersonSurrogated)  
    {  
        PersonSurrogated personSurrogated = (PersonSurrogated)obj;  
        Person person = new Person();  
        person.firstName = personSurrogated.FirstName;  
        person.lastName = personSurrogated.LastName;  
        person.age = personSurrogated.Age;  
        return person;  
    }  
    return obj;  
}  
```  
  
 <span data-ttu-id="24095-124">Para mapear o `PersonSurrogated` de contrato de dados para existente `Person` classe durante a importação de esquema, o exemplo implementa o <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%28System.String%2CSystem.String%2CSystem.Object%29> método, conforme mostrado no código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="24095-124">To map the `PersonSurrogated` data contract to the existing `Person` class during schema import, the sample implements the <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%28System.String%2CSystem.String%2CSystem.Object%29> method, as shown in the following sample code.</span></span>  
  
```  
public Type GetReferencedTypeOnImport(string typeName,   
               string typeNamespace, object customData)  
{  
if (  
typeNamespace.Equals("http://schemas.datacontract.org/2004/07/DCSurrogateSample")  
)  
    {  
         if (typeName.Equals("PersonSurrogated"))  
        {  
             return typeof(Person);  
        }  
     }  
     return null;  
}  
```  
  
 <span data-ttu-id="24095-125">O seguinte código de exemplo conclui a implementação de <xref:System.Runtime.Serialization.IDataContractSurrogate> interface.</span><span class="sxs-lookup"><span data-stu-id="24095-125">The following sample code completes the implementation of the <xref:System.Runtime.Serialization.IDataContractSurrogate> interface.</span></span>  
  
```  
public System.CodeDom.CodeTypeDeclaration ProcessImportedType(  
          System.CodeDom.CodeTypeDeclaration typeDeclaration,   
          System.CodeDom.CodeCompileUnit compileUnit)  
{  
    return typeDeclaration;  
}  
public object GetCustomDataToExport(Type clrType,   
                               Type dataContractType)  
{  
    return null;  
}  
  
public object GetCustomDataToExport(  
System.Reflection.MemberInfo memberInfo, Type dataContractType)  
{  
    return null;  
}  
public void GetKnownCustomDataTypes(  
        KnownTypeCollection customDataTypes)  
{  
    // It does not matter what we do here.  
    throw new NotImplementedException();  
}  
```  
  
 <span data-ttu-id="24095-126">Neste exemplo, o substituto está habilitado no ServiceModel por um atributo chamado `AllowNonSerializableTypesAttribute`.</span><span class="sxs-lookup"><span data-stu-id="24095-126">In this sample, the surrogate is enabled in ServiceModel by an attribute called `AllowNonSerializableTypesAttribute`.</span></span> <span data-ttu-id="24095-127">Os desenvolvedores precisam aplicar esse atributo no seu contrato de serviço, conforme mostrado no `IPersonnelDataService` acima do contrato de serviço.</span><span class="sxs-lookup"><span data-stu-id="24095-127">Developers would need to apply this attribute on their service contract as shown on the `IPersonnelDataService` service contract above.</span></span> <span data-ttu-id="24095-128">Esse atributo implementa `IContractBehavior` e configura o substituto em operações em seu `ApplyClientBehavior` e `ApplyDispatchBehavior` métodos.</span><span class="sxs-lookup"><span data-stu-id="24095-128">This attribute implements `IContractBehavior` and sets up the surrogate on operations in its `ApplyClientBehavior` and `ApplyDispatchBehavior` methods.</span></span>  
  
 <span data-ttu-id="24095-129">O atributo não é necessário nesse caso - ele é usado para fins de demonstração neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="24095-129">The attribute is not necessary in this case - it is used for demonstration purposes in this sample.</span></span> <span data-ttu-id="24095-130">Os usuários também podem habilitar um substituto adicionando manualmente semelhantes `IContractBehavior`, `IEndpointBehavior` ou `IOperationBehavior` usando código ou usando a configuração.</span><span class="sxs-lookup"><span data-stu-id="24095-130">Users can alternatively enable a surrogate by manually adding a similar `IContractBehavior`, `IEndpointBehavior` or `IOperationBehavior` using code or using configuration.</span></span>  
  
 <span data-ttu-id="24095-131">O `IContractBehavior` implementação procura por operações que usam DataContract, verificando se eles têm um `DataContractSerializerOperationBehavior` registrado.</span><span class="sxs-lookup"><span data-stu-id="24095-131">The `IContractBehavior` implementation looks for operations that use DataContract by checking if they have a `DataContractSerializerOperationBehavior` registered.</span></span> <span data-ttu-id="24095-132">Se isso ocorrer, ele define o `DataContractSurrogate` propriedade esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="24095-132">If they do, it sets the `DataContractSurrogate` property on that behavior.</span></span> <span data-ttu-id="24095-133">O código de exemplo a seguir mostra como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="24095-133">The following sample code shows how this is done.</span></span> <span data-ttu-id="24095-134">Configuração do substituto nesse comportamento da operação habilitada para serialização e desserialização.</span><span class="sxs-lookup"><span data-stu-id="24095-134">Setting the surrogate on this operation behavior enables it for serialization and deserialization.</span></span>  
  
```  
public void ApplyClientBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime proxy)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
public void ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.DispatchRuntime dispatch)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
private static void ApplyDataContractSurrogate(OperationDescription description)  
{  
    DataContractSerializerOperationBehavior dcsOperationBehavior = description.Behaviors.Find<DataContractSerializerOperationBehavior>();  
    if (dcsOperationBehavior != null)  
    {  
        if (dcsOperationBehavior.DataContractSurrogate == null)  
            dcsOperationBehavior.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
    }  
}  
```  
  
 <span data-ttu-id="24095-135">Etapas adicionais precisam ser tomadas para plug-in do substituto para uso durante a geração de metadados.</span><span class="sxs-lookup"><span data-stu-id="24095-135">Additional steps need to be taken to plug in the surrogate for use during metadata generation.</span></span> <span data-ttu-id="24095-136">Um mecanismo para fazer isso é fornecer um `IWsdlExportExtension` que é o que demonstra este exemplo.</span><span class="sxs-lookup"><span data-stu-id="24095-136">One mechanism to do this is to provide an `IWsdlExportExtension` which is what this sample demonstrates.</span></span> <span data-ttu-id="24095-137">É outra maneira de modificar o `WsdlExporter` diretamente.</span><span class="sxs-lookup"><span data-stu-id="24095-137">Another way is to modify the `WsdlExporter` directly.</span></span>  
  
 <span data-ttu-id="24095-138">O `AllowNonSerializableTypesAttribute` atributo implementa `IWsdlExportExtension` e `IContractBehavior`.</span><span class="sxs-lookup"><span data-stu-id="24095-138">The `AllowNonSerializableTypesAttribute` attribute implements `IWsdlExportExtension` and `IContractBehavior`.</span></span> <span data-ttu-id="24095-139">A extensão pode ser um `IContractBehavior` ou `IEndpointBehavior` nesse caso.</span><span class="sxs-lookup"><span data-stu-id="24095-139">The extension can be either an `IContractBehavior` or `IEndpointBehavior` in this case.</span></span> <span data-ttu-id="24095-140">Seu `IWsdlExportExtension.ExportContract` implementação do método permite que o substituto adicionando-o para o `XsdDataContractExporter` usado durante a geração de esquema para DataContract.</span><span class="sxs-lookup"><span data-stu-id="24095-140">Its `IWsdlExportExtension.ExportContract` method implementation enables the surrogate by adding it to the `XsdDataContractExporter` used during schema generation for DataContract.</span></span> <span data-ttu-id="24095-141">O trecho de código a seguir mostra como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="24095-141">The following code snippet shows how to do this.</span></span>  
  
```  
public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)  
{  
    if (exporter == null)  
        throw new ArgumentNullException("exporter");  
  
    object dataContractExporter;  
    XsdDataContractExporter xsdDCExporter;  
    if (!exporter.State.TryGetValue(typeof(XsdDataContractExporter), out dataContractExporter))  
    {  
        xsdDCExporter = new XsdDataContractExporter(exporter.GeneratedXmlSchemas);  
        exporter.State.Add(typeof(XsdDataContractExporter), xsdDCExporter);  
    }  
    else  
    {  
        xsdDCExporter = (XsdDataContractExporter)dataContractExporter;  
    }  
    if (xsdDCExporter.Options == null)  
        xsdDCExporter.Options = new ExportOptions();  
  
    if (xsdDCExporter.Options.DataContractSurrogate == null)  
        xsdDCExporter.Options.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
}  
```  
  
 <span data-ttu-id="24095-142">Quando você executar o exemplo, o cliente chama AddEmployee seguido por uma chamada de GetEmployee para verificar se a primeira chamada foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="24095-142">When you run the sample, the client calls AddEmployee followed by a GetEmployee call to check if the first call was successful.</span></span> <span data-ttu-id="24095-143">O resultado da solicitação de operação GetEmployee é exibido na janela do console do cliente.</span><span class="sxs-lookup"><span data-stu-id="24095-143">The result of the GetEmployee operation request is displayed in the client console window.</span></span> <span data-ttu-id="24095-144">A operação de GetEmployee deve localizar o funcionário com êxito e imprimir "encontrado".</span><span class="sxs-lookup"><span data-stu-id="24095-144">The GetEmployee operation must succeed in finding the employee and print "found".</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="24095-145">Este exemplo mostra como conectar um substituto de serialização, desserializar e geração de metadados.</span><span class="sxs-lookup"><span data-stu-id="24095-145">This sample shows how to plug in a surrogate for serialize, deserialize and metadata generation.</span></span> <span data-ttu-id="24095-146">Ele não mostra como conectar um substituto para geração de código de metadados.</span><span class="sxs-lookup"><span data-stu-id="24095-146">It does not show how to plug in a surrogate for code generation from metadata.</span></span> <span data-ttu-id="24095-147">Para ver um exemplo de como um substituto pode ser usado para conectar à geração de código de cliente, consulte o [publicação de WSDL personalizado](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md) exemplo.</span><span class="sxs-lookup"><span data-stu-id="24095-147">To see a sample of how a surrogate can be used to plug into client code generation, see the [Custom WSDL Publication](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md) sample.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="24095-148">Para configurar, compilar, e executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="24095-148">To set up, build, and run the sample</span></span>  
  
1.  <span data-ttu-id="24095-149">Certifique-se de que você executou o [único procedimento de instalação para os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24095-149">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2.  <span data-ttu-id="24095-150">Para compilar o c# edition da solução, siga as instruções em [compilar os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24095-150">To build the C# edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
3.  <span data-ttu-id="24095-151">Para executar o exemplo em uma configuração ou entre computadores, siga as instruções em [executando os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24095-151">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="24095-152">Os exemplos podem já estar instalados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="24095-152">The samples may already be installed on your machine.</span></span> <span data-ttu-id="24095-153">Verifique o seguinte diretório (padrão) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="24095-153">Check for the following (default) directory before continuing.</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  <span data-ttu-id="24095-154">Se este diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos do Windows Workflow Foundation (WF) para o .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos.</span><span class="sxs-lookup"><span data-stu-id="24095-154">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) to download all [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="24095-155">Este exemplo está localizado no seguinte diretório.</span><span class="sxs-lookup"><span data-stu-id="24095-155">This sample is located in the following directory.</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\DataContract`  
  
## <a name="see-also"></a><span data-ttu-id="24095-156">Consulte também</span><span class="sxs-lookup"><span data-stu-id="24095-156">See Also</span></span>