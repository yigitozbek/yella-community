## What is Yella Community?

* Yella Framework provides you with an infrastructure by providing you with the latest technology in a fast and efficient way while you are making a web project. Yella Community offers many conveniences to developers as it is free.

* If there is a deleted data, it ensures that the data is not returned without writing any code instead of constantly writing to the condition so that the data does not come.

## You can see a few of these conveniences below.

```c#
public class Order : FullAuditedEntity<Guid> 
{

  ...
  
}
```

```c#
[Authorize]
public class OrderApplicationService : ApplicationService, IOrderService
{

    private readonly IRepository<Order, Guid> _orderRepository;

    public OrderApplicationService(IRepository<Order, Guid> orderRepository)
    {
        _orderRepository = orderRepository;
    }

    ...
    
}
```
```c#
[TransactionAspect(AspectPriority = 3)]
[AuthorizationAspect(YellaPermission.Orders.Update, AspectPriority = 1)]
[FluentValidationAspect(typeof(OrderUpdateRequestValidator), AspectPriority = 2)]
public async Task<IDataResult<OrderUpdateResponse>> UpdateAsync(OrderUpdateRequest input)
{

  IQueryable<Order> query = await _orderRepository.WithIncludeAsync(x => x.SalesRepresentative);
  
  ...

}
```

```c#
[AuthorizationAspect(YellaPermission.Demands.Get, AspectPriority = 1)]
public async Task<IDataResult<IEnumerable<DemandDto>>> GetListFilterAsync(List<IFilterInput> input)
{
    var query = (await _demandRepository.WithIncludeAsync(x => x.Customer);

    var list = await (await query.FilterAsync(input)).ToListAsync();

    return ReturnResult(list.ToMapper<IEnumerable<DemandDto>>());
}
```


## Support US

* If you like the Yella, you can become a sponsor.

Donate using cryptocurrencies:
- ```BTC: 39Hse93PpgJCko4XdwKt5modXp1oKUFXcX```
- ```ETH: 0x21D20b052e9546a0Eb267B08828d185250767976```


