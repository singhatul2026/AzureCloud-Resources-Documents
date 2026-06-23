## What is Azure Load Balancer?

Azure Load Balancer is a **networking service** that distributes incoming traffic across multiple backend resources (VMs). Its main job is to provide high availability and scalability — if you have multiple VMs running the same application, the Load Balancer evenly distributes traffic among them, so no single VM gets overloaded, and if one VM goes down, traffic is automatically routed to another healthy VM.

It operates at **Layer 4** (TCP/UDP) — meaning it only looks at IP address and port, not application-level content (like HTTP headers). That's why it's extremely fast.

## Types of Azure Load Balancer

**1. Based on accessibility:**

- **Public Load Balancer**: Handles internet-facing traffic. It has a public IP, so requests coming from outside the internet get distributed to backend VMs. (Example: a website accessible from the internet)

- **Internal Load Balancer (ILB)**: Used only for **private/internal traffic** — within a VNet. It uses a private IP. Used when you need to load balance internal applications (like a database tier or backend services) that shouldn't be directly accessible from the internet.

**2. Based on SKU (pricing tier/features):**

- **Basic Load Balancer**: Free, with limited features, suited for small/dev workloads. (Microsoft is deprecating this — it will be retired by September 2025)
- **Standard Load Balancer**: Production-grade, supports zone-redundancy, better SLA, security (default deny), and higher scale. This is what's used in production setups today.

## Use (Purpose) of Azure Load Balancer

1. **High Availability**: If one VM fails, traffic is automatically routed to other healthy VMs
2. **Load Distribution**: Evenly distributes traffic across multiple VMs to improve performance
3. **Scalability**: As traffic grows, you can add more VMs behind the load balancer
4. **Health Monitoring**: Continuously checks the health of backend VMs and stops sending traffic to unhealthy ones
5. **Port Forwarding/NAT**: Also used to forward specific ports to specific VMs

## Components of Azure Load Balancer

1. **Frontend IP Configuration**: The IP address where client traffic is sent — can be a public or private IP

2. **Backend Pool**: A group of VMs or VM scale sets that actually process the traffic. The load balancer distributes traffic within this pool

3. **Health Probes**: Periodically checks whether backend VMs are "healthy" (responding or not). If a VM is unhealthy, the load balancer stops sending it traffic

4. **Load Balancing Rules**: Defines how traffic coming in on a frontend IP+port gets routed to a backend pool and port. The distribution algorithm (default: 5-tuple hash — source IP, source port, destination IP, destination port, protocol) is also decided here

5. **Inbound NAT Rules**: Used to forward traffic on a specific port to a specific VM's specific port (e.g., RDP/SSH access for individual VMs)

6. **Outbound Rules**: Configures outbound internet connectivity (SNAT - Source NAT) for VMs in the backend pool

---

### Quick analogy:

Think of a restaurant where one waiter (the Load Balancer's "frontend") takes customers (traffic) and sends them to different chefs (backend VMs) based on who's available. The waiter regularly checks which chefs are currently able to work (health probe), and if a chef is busy or absent, traffic goes to another chef instead.

In the context of your Azure DevOps + Terraform learning, when you build production-style infrastructure (like that URL Shortener API with potentially multiple VM instances), the Load Balancer would play this exact role — routing traffic to the right VM.



## Azure Load Balancer kya hai?

Load Balancer ek **networking service** hai jo incoming traffic ko multiple backend resources (VMs) mein distribute karta hai. Iska kaam hai high availability aur scalability provide karna — matlab agar tumhare paas multiple VMs hain ek hi application ke liye, toh Load Balancer traffic ko evenly split karta hai unke beech, taaki ek VM overload na ho aur agar ek VM down ho jaaye toh traffic automatically doosri healthy VM pe chala jaaye.

Yeh **Layer 4** (TCP/UDP) pe kaam karta hai — matlab yeh sirf IP address aur port dekhta hai, application content (jaise HTTP headers) nahi dekhta. Isliye yeh bohot fast hota hai.

## Types of Azure Load Balancer

**1. Based on accessibility:**

- **Public Load Balancer**: Internet-facing traffic ko handle karta hai. Public IP hota hai isme, jisse outside internet se requests andar aati hain aur backend VMs mein distribute hoti hain. (Example: tumhara website jo internet se accessible hai)

- **Internal Load Balancer (ILB)**: Sirf **private/internal traffic** ke liye — VNet ke andar hi. Yeh private IP use karta hai. Use hota hai jab internal applications (jaise database tier, backend services) ko load balance karna ho, jo internet se directly accessible nahi hone chahiye.

**2. Based on SKU (pricing tier/features):**

- **Basic Load Balancer**: Free, limited features, chhote/dev workloads ke liye. (Microsoft deprecate kar raha hai isko — Sept 2025 tak retire ho jayega)
- **Standard Load Balancer**: Production-grade, zone-redundancy support, better SLA, security (default deny), aur higher scale. Aaj kal sab production setups mein yeh use hota hai.

## Use (Purpose) of Azure Load Balancer

1. **High Availability**: Agar ek VM fail ho jaaye, traffic automatically baaki healthy VMs pe route ho jata hai
2. **Load Distribution**: Traffic ko evenly multiple VMs mein baant deta hai, taaki performance better rahe
3. **Scalability**: Jab traffic badhe, naye VMs add karke load balancer ke peeche daal sakte ho
4. **Health Monitoring**: Backend VMs ki health check karta hai, aur unhealthy VM ko traffic bhejna band kar deta hai
5. **Port Forwarding/NAT**: Specific ports ko specific VM tak forward karne ke liye bhi use hota hai

## Components of Azure Load Balancer

1. **Frontend IP Configuration**: Yeh wo IP address hai jahan client traffic bhejta hai — public ya private IP ho sakta hai

2. **Backend Pool**: VMs ya VM scale sets ka group jo actual traffic ko process karte hain. Load balancer traffic ko isi pool ke andar distribute karta hai

3. **Health Probes**: Yeh periodically backend VMs ko check karta hai ki woh "healthy" hain ya nahi (response de rahe hain ya nahi). Agar VM unhealthy ho, toh load balancer usko traffic bhejna stop kar deta hai

4. **Load Balancing Rules**: Yeh define karta hai ki frontend IP+port se aane wala traffic kis backend pool aur port pe jaayega. Distribution algorithm (default: 5-tuple hash — source IP, source port, dest IP, dest port, protocol) bhi yahi decide karta hai

5. **Inbound NAT Rules**: Specific port pe aane wala traffic kisi specific VM ke specific port pe forward karne ke liye (jaise RDP/SSH access for individual VMs)

6. **Outbound Rules**: Backend pool ke VMs ko internet pe outbound connectivity dene ke liye (SNAT - Source NAT) configure karta hai

---

### Quick analogy samajhne ke liye:

Socho ek restaurant hai jisme ek hi waiter (Load Balancer ka "frontend") customers (traffic) leta hai, aur unko alag-alag chefs (backend VMs) ke paas bhejta hai based on kaun free hai. Waiter regularly check karta rehta hai kaunsa chef abhi kaam kar sakta hai (health probe), aur agar koi chef busy/absent hai, traffic doosre chef ko milta hai.

Tumhare Azure DevOps + Terraform learning ke context mein, jab tum production-style infra banaoge (jaise wo URL Shortener API jisme multiple VM instances ho sakte hain), Load Balancer wahi role play karega jo traffic ko sahi VM tak route karega.
