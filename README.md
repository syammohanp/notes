SOLID: OOPs Design Priciples
Single Responsiblity: A class should have only one reason to change
interface/class defenition with only related props and member functions
Open Cloded:Classes should be open for extension, but closed for modifications
Fully good with Liskov's substitution also. If the implementaiton is only for employee type converted to abstract class it solved Open Closed. 
IEmployee, IBonus, Abstract Employee:IEmployee, IBounus, PermenentEmp:Employee, TempEmp:Employee, ContractEmp:IEmployee
Liskov Substitution: S is a subtype of B. Objects of type B may be replaced with object of S. Derived objects must be completely substitutable for their base objects. ObjBase Base = new Derived()
IEmployee, IBonus, Abstract Employee:IEmployee, IBounus, PermenentEmp:Employee, TempEmp:Employee, ContractEmp:IEmployee
Interface Segrigation:No client should be forced to depend on method it does not use. See with printer option and fat interfaces needs to be split to many smaller interfaces.
Dependency Inversion:High level modules should not depend on low-level modules. Both should depend on abstractions. 
public interface IDAL {void Save(Object obj)}
public class DAL:IDAL {public void Save(Object obj){//Save logic}}
public class BLL{private readonly IDAL _dal; 
public BLL(IDAL dal) {
    _dal = dal;
}
public void SavefromClient(object obj) {_dal.Save(obj);}
}
MicroServices:
Monolethic architecutre is like a big container where in all the software components of an application are assembled together and tightly packaged