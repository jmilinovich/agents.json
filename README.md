# agents.json Specification (RFC)

## Vision
The web is evolving from a human-first interface to one that serves both humans and artificial agents. While protocols like robots.txt and sitemap.xml help web crawlers understand site structure, we lack a standardized way for websites to declare their agent-interaction capabilities. This specification defines agents.json, a protocol enabling websites to describe how artificial agents can interact with them programmatically and securely.

As Dharmesh Shah, Founder and CTO at HubSpot, noted:
> "I love APIs, but as we move towards a more agent-based world, I think we'll see forward-thinking products and platforms offer an interface that's built for agents."

This specification aims to bridge the gap between traditional human-oriented websites and the emerging ecosystem of AI agents, providing a standard way for websites to declare their agent capabilities and for agents to discover and interact with those capabilities.

## Specification

### Discovery
- Primary location: `/agents.json`
- File must be valid JSON

### Schema
```json
{
  "version": "1.0",
  "site_info": {
    "name": "string",
    "description": "string",
    "home_url": "string"
  },

  "authentication": {
    "required": boolean,
    "methods": [{
      "type": "string",
      "documentation_url": "string"
    }]
  },

  "intents": {
    "supported": [{
      "type": "string",
      "description": "string",
      "authentication_required": boolean,
      "rate_limits": {
        "requests_per_minute": number
      },
      "endpoints": [{
        "path": "string",
        "methods": ["string"],
        "documentation_url": "string"
      }],
      "examples": [{
        "description": "string",
        "request": {},
        "response": {}
      }]
    }]
  },

  "policies": {
    "rate_limits": {
      "requests_per_minute": number
    },
    "agent_identification": {
      "required": boolean,
      "method": "string"
    }
  }
}
```

### Intent Types
Intent types are free-form strings that describe the capability being offered. Sites should use whatever intent types best describe their capabilities. While you're free to define your own intent types, some common patterns might include:

- Reading content
- Creating or modifying content
- Searching or filtering information
- Making state changes
- Setting up ongoing interactions

These are suggestions only. The power of this specification lies in its flexibility to accommodate both current and future use cases.

## Examples

### E-commerce Site
The repository includes an example agents.json for an e-commerce site (ExecuSystems) that demonstrates how to expose product browsing, shopping cart management, and checkout capabilities. Key features shown:

- Product catalog browsing and search
- Detailed product information retrieval
- Shopping cart management
- Checkout process
- Customer service contact methods

See `examples/shop-agents.json` for the complete implementation.

### Personal Blog
The repository also includes an example for a personal blog site that shows how to expose content reading and subscription capabilities. Key features shown:

- Blog post listing and retrieval
- Content subscription system
- Simple authentication-free access
- Clear rate limiting policies

See `examples/blog-agents.json` for the complete implementation.

## Status
This is an early draft specification. All aspects are open for discussion and revision based on community feedback and real-world implementation experience.

## Contributing
Have thoughts? Open an issue to discuss or post on x.com. 
- Use cases you're excited about
- Challenges you foresee
- Suggestions for improvement
- Implementation ideas and examples
- Additional real-world examples of agents.json implementations

Let's shape this together!