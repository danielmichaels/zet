# WGD Fri 2022-05-06

Preparing Mudmap for a big change and researching account grouping functionality.

## Mudmap

Mudmap's underlying API has seen a big update and I spent a fair chunk of time 
testing it to make sure no breaking changes are introduced.

I can now create a Go client from the `openapi.json` the API provides. But, I find the
auto generating tools to create really unwieldy code. I guess that is the point, its 
a contract between the API and the client. Nonetheless, I'm not going to use the tools 
I've tried but instead just use it to influence who *I* build each endpoint. 

Also, I started researching and thinking through how I am going to create an account 
hierarchy within Mudmap. Users want to have *teams* or *groups* with RBAC policies. 
Since I use Auth0 as my authentication provider, I am somewhat pigeon holed to 
use their methods. From what I can tell so far, their Organisations product is not
what I want. It is also too expensive. Instead I am looking at creating some custom 
wrapping code to extend their *groups* extension with my own database. Research continues
as there are some considerations such a latency here.

Wrote the April retrospective but haven't published it yet. Still need to proof it
and make sure the standard grammar issues are fixed up. 

Released a number of small updates for my [zet-cmd] package. Really enjoying working
on it *and* using it to catalogue my thoughts. People can freely read it which is fine 
but I feel zero regrets from the poor wording or brain spew that gets placed there.

## Conclusion

Worked nearly 50 hours this week on a big deployment. It's bloody frustrating working in the
constrained environment I call work. Aside from that, it has been a good pairing with a much more senior engineer during the process. 

[zet-cmd]: https://github.com/danielmichaels/zet-cmd

