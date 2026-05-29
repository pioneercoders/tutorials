# CDN (Content Delivery Network)

CDN is a distributed network of servers that deliver web content to users based on their geographic location, origin server, and the content delivery server.

## Introduction

CDN (Content Delivery Network) is a distributed network of servers that deliver web content to users based on their geographic location, origin server, and the content delivery server. CDNs cache static content like images, videos, CSS, JavaScript, and other assets on edge servers located around the world. When a user requests content, the CDN serves it from the nearest edge server, reducing latency and improving performance. CDNs also handle high traffic loads, reduce bandwidth costs, and provide security features like DDoS protection. Popular CDN providers include Cloudflare, AWS CloudFront, Akamai, Fastly, and Cloudflare. CDNs use techniques like anycast routing, geographic DNS, and cache optimization to deliver content efficiently. They are essential for global applications, media streaming, e-commerce, and any system serving static content to a distributed user base.

**Why CDN Matters:**
- Reduces latency through geographic proximity
- Improves user experience globally
- Handles high traffic loads
- Reduces bandwidth costs
- Provides security features
- Protects origin server from overload

**Where It Is Used:**
- Static asset delivery (images, CSS, JS)
- Video streaming (Netflix, YouTube)
- Software distribution (downloads)
- API response caching
- E-commerce platforms
- Global web applications

## Core Concept Explanation

CDN works by distributing content across a network of edge servers located in various geographic locations. When a user requests content, the CDN routes the request to the nearest edge server. If the content is cached on that edge server, it's served immediately (cache hit). If not, the edge server fetches the content from the origin server, caches it, and serves it to the user (cache miss). The CDN uses DNS-based routing, anycast, or geographic DNS to direct users to the nearest edge server. Content is cached based on cache headers (Cache-Control, Expires) and can be invalidated through TTL expiration, explicit invalidation, or versioning. CDNs also provide edge computing capabilities, allowing code to run at the edge for dynamic content generation, request transformation, and security filtering.

**Step-by-Step Breakdown:**
1. User requests content from your domain
2. DNS resolves to CDN edge server
3. Edge server checks cache for content
4. If cache hit, serve content immediately
5. If cache miss, fetch from origin server
6. Cache content on edge server
7. Serve content to user
8. Update cache based on cache headers
9. Monitor performance and cache hit rate

**Intuition Behind the Concept:**
Think of CDN like having warehouses (edge servers) in different cities instead of one central warehouse. When a customer orders a product, it's shipped from the nearest warehouse instead of the central one, reducing delivery time. The warehouses keep popular items in stock (cache). When a new item is ordered, it's shipped from the central warehouse and stocked in the local warehouse for future orders. This is much faster than shipping everything from one central location.

**Visual Thinking:**
```
User Request Flow:
User → DNS → CDN Edge Server → Origin Server
         ↓         ↓
    Geographic   Cache Check
    Routing       ↓
              Cache Hit → Serve
              Cache Miss → Fetch from Origin
                           ↓
                      Cache & Serve

CDN Network:
Global Users → Multiple Edge Servers → Origin Server
     ↓              ↓                    ↓
  US East        Europe              Asia
  US West        South America       Australia
  etc.           etc.                etc.
```

## Internal Working / Logic

CDN operates through a distributed network of edge servers that cache and serve content. When a user requests content, DNS resolution directs them to the nearest edge server based on geographic location, network conditions, or server load. The edge server checks its cache for the requested content. If found (cache hit), it serves the content immediately. If not found (cache miss), it fetches the content from the origin server, caches it based on cache headers, and serves it to the user. The CDN uses cache headers like Cache-Control, Expires, ETag, and Last-Modified to determine caching behavior. Cache invalidation can be time-based (TTL), explicit (purge API), or version-based (URL versioning). CDNs also provide edge computing capabilities through edge workers or serverless functions that can run code at the edge for dynamic content generation, request transformation, security filtering, and A/B testing.

**Operation 1: Content Delivery (Cache Hit)**
- User requests content
- DNS resolves to nearest edge server
- Edge server checks cache
- Content found in cache
- Edge server serves content immediately
- User receives content with low latency
- CDN logs the request

**Operation 2: Content Delivery (Cache Miss)**
- User requests content
- DNS resolves to nearest edge server
- Edge server checks cache
- Content not found in cache
- Edge server fetches from origin server
- Origin server returns content
- Edge server caches content
- Edge server serves content to user
- User receives content with slightly higher latency

**Operation 3: Cache Invalidation**
- Content updated on origin server
- CDN purges content from edge servers
- Or wait for TTL expiration
- Or use versioned URLs
- Next request fetches fresh content
- Content recached on edge servers

**Operation 4: Edge Computing**
- User requests dynamic content
- Edge worker processes request
- Edge worker may transform request
- Edge worker may call external APIs
- Edge worker generates response
- Response served from edge
- Low latency for dynamic content

**Flow Explanation (Content Delivery):**
1. User requests content via URL
2. DNS resolves to CDN edge server
3. Edge server receives request
4. Edge server checks cache
5. If cache hit, serve immediately
6. If cache miss, fetch from origin
7. Cache content based on headers
8. Serve content to user
9. Log request for analytics

**Decision Making Logic:**
The key decisions are:
- Which edge server to route to (geographic, load-based)
- Whether to cache content (based on headers, content type)
- How long to cache (TTL based on cache headers)
- How to invalidate cache (TTL, purge, versioning)
- Whether to use edge computing (dynamic content needs)
- How to handle errors (fallback to origin, error pages)

## Algorithm / Approach

**CDN Routing Algorithm**

```
1. User requests content
2. DNS resolves to CDN
3. CDN selects nearest edge server
4. Edge server checks cache
5. If cache hit, serve content
6. If cache miss, fetch from origin
7. Cache content based on headers
8. Serve content to user
```

**Cache Selection Algorithm**

```
1. Parse cache headers
2. Determine cacheability
3. Set TTL based on headers
4. Cache content if cacheable
5. Set expiration time
6. Track cache hits/misses
```

**Cache Invalidation Algorithm**

```
1. Detect content change
2. Purge from edge servers
3. Or wait for TTL expiration
4. Or use versioned URLs
5. Force cache refresh
6. Update cache with fresh content
```

**Edge Computing Algorithm**

```
1. Edge worker receives request
2. Parse and validate request
3. Transform request if needed
4. Call external APIs if needed
5. Generate response
6. Cache response if appropriate
7. Return response to user
```

## Implementations

### 1. Cache Headers Configuration

```javascript
const express = require('express');
const app = express();

// Configure static file serving with cache headers
app.use(express.static('public', {
  maxAge: '1y', // 1 year for static assets
  etag: true, // Enable ETag
  lastModified: true, // Enable Last-Modified
  setHeaders: (res, path) => {
    // HTML files should not be cached long
    if (path.endsWith('.html')) {
      res.setHeader('Cache-Control', 'public, max-age=0, must-revalidate');
    }
    // CSS and JS files can be cached longer
    else if (path.match(/\.(css|js)$/)) {
      res.setHeader('Cache-Control', 'public, max-age=31536000, immutable');
    }
    // Images can be cached very long
    else if (path.match(/\.(png|jpg|jpeg|gif|svg|webp)$/)) {
      res.setHeader('Cache-Control', 'public, max-age=31536000, immutable');
    }
  }
}));

app.listen(3000);
```

**Advantages:**
- Simple configuration
- Browser caching
- Reduced server load
- Better performance

### 2. Edge Worker Implementation

```javascript
// Cloudflare Worker
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)
  
  // Cache static assets
  if (url.pathname.match(/\.(css|js|png|jpg|jpeg|gif|svg|webp)$/)) {
    const cache = caches.default
    const cached = await cache.match(request)
    
    if (cached) {
      return cached
    }
    
    const response = await fetch(request)
    const responseToCache = new Response(response.clone().body, response)
    responseToCache.headers.set('Cache-Control', 'public, max-age=31536000, immutable')
    await cache.put(request, responseToCache)
    
    return response
  }
  
  // Transform API responses
  if (url.pathname.startsWith('/api/')) {
    const response = await fetch(request)
    const data = await response.json()
    
    // Add CDN-specific headers
    const transformed = new Response(JSON.stringify(data), {
      headers: {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*',
        'X-CDN-Cache': 'MISS'
      }
    })
    
    return transformed
  }
  
  return fetch(request)
}
```

**Advantages:**
- Run code at edge
- Transform requests/responses
- Custom caching logic
- Security filtering

### 3. Cache Invalidation Strategy

```javascript
class CacheInvalidator {
  constructor(cdnClient) {
    this.cdnClient = cdnClient;
  }
  
  // Purge specific URL
  async purgeUrl(url) {
    try {
      await this.cdnClient.purgeUrl(url);
      console.log(`Purged: ${url}`);
    } catch (error) {
      console.error(`Failed to purge ${url}:`, error);
    }
  }
  
  // Purge multiple URLs
  async purgeUrls(urls) {
    try {
      await this.cdnClient.purgeUrls(urls);
      console.log(`Purged ${urls.length} URLs`);
    } catch (error) {
      console.error('Failed to purge URLs:', error);
    }
  }
  
  // Purge by tag
  async purgeTag(tag) {
    try {
      await this.cdnClient.purgeTag(tag);
      console.log(`Purged tag: ${tag}`);
    } catch (error) {
      console.error(`Failed to purge tag ${tag}:`, error);
    }
  }
  
  // Purge all content
  async purgeAll() {
    try {
      await this.cdnClient.purgeAll();
      console.log('Purged all content');
    } catch (error) {
      console.error('Failed to purge all:', error);
    }
  }
}

// Usage
const invalidator = new CacheInvalidator(cdnClient);

// On content update
await invalidator.purgeUrl('https://example.com/style.css');
await invalidator.purgeTag('product-pages');
```

**Advantages:**
- Explicit cache control
- Immediate invalidation
- Tag-based purging
- Bulk operations

### 4. Version-Based Caching

```javascript
const express = require('express');
const app = express();
const crypto = require('crypto');

// Generate content hash for versioning
function generateContentHash(content) {
  return crypto.createHash('md5').update(content).digest('hex').substring(0, 8);
}

// Serve versioned static assets
app.get('/static/:version/:file', (req, res) => {
  const { version, file } = req.params;
  const filePath = `./public/${file}`;
  
  // Validate version (optional)
  // Serve file
  res.sendFile(filePath, {
    maxAge: '1y',
    immutable: true
  });
});

// Generate versioned URLs in templates
function getVersionedUrl(file, content) {
  const hash = generateContentHash(content);
  return `/static/${hash}/${file}`;
}

// Example HTML
const cssContent = 'body { background: blue; }';
const cssUrl = getVersionedUrl('style.css', cssContent);
console.log(cssUrl); // /static/a1b2c3d4/style.css
```

**Advantages:**
- Automatic cache busting
- Long cache times
- No invalidation needed
- Simple implementation

### 5. Dynamic Caching with Edge Computing

```javascript
// Edge worker for dynamic content caching
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)
  const cacheKey = `dynamic:${url.pathname}`
  const cache = caches.default
  
  // Check cache
  const cached = await cache.match(cacheKey)
  if (cached) {
    return cached
  }
  
  // Fetch from origin
  const response = await fetch(request)
  const data = await response.json()
  
  // Transform data
  const transformed = {
    ...data,
    timestamp: Date.now(),
    cdnCached: true
  }
  
  // Cache for 5 minutes
  const responseToCache = new Response(JSON.stringify(transformed), {
    headers: {
      'Content-Type': 'application/json',
      'Cache-Control': 'public, max-age=300',
      'X-CDN-Cache': 'MISS'
    }
  })
  
  await cache.put(cacheKey, responseToCache)
  
  return responseToCache
}
```

**Advantages:**
- Cache dynamic content
- Reduce origin load
- Transform at edge
- Better performance

## Dry Run

**Example: CDN Content Delivery**

**Request:**
```
GET https://example.com/style.css
User Location: New York, USA
```

**Step-by-Step Execution:**

```
1. User requests style.css
2. DNS resolves to CDN
3. CDN selects New York edge server
4. Edge server checks cache for style.css
5. Cache miss - not cached
6. Edge server fetches from origin server
7. Origin server returns style.css
8. Edge server caches style.css (TTL: 1 year)
9. Edge server serves style.css to user
10. User receives style.css (latency: 50ms)

Second request (same user, 1 hour later):
1. User requests style.css
2. DNS resolves to CDN
3. CDN selects New York edge server
4. Edge server checks cache for style.css
5. Cache hit - found in cache
6. Edge server serves style.css immediately
7. User receives style.css (latency: 10ms)
```

**Request/Response Table:**

| Step | Component | Action | Status |
|------|-----------|--------|--------|
| 1 | User | Request style.css | - |
| 2 | DNS | Resolve to CDN | New York edge |
| 3 | Edge Server | Check cache | Miss |
| 4 | Edge Server | Fetch from origin | - |
| 5 | Origin Server | Return style.css | 200 OK |
| 6 | Edge Server | Cache content | TTL: 1 year |
| 7 | Edge Server | Serve to user | 200 OK |
| 8 | User | Receive content | Latency: 50ms |
| 9 | User | Request style.css | - |
| 10 | Edge Server | Check cache | Hit |
| 11 | Edge Server | Serve from cache | 200 OK |
| 12 | User | Receive content | Latency: 10ms |

## Edge Cases

### 1. Cache Stampede
```javascript
// Multiple requests miss cache simultaneously
// All hit origin server
// Solution: Cache warming, request coalescing
```

### 2. Origin Overload
```javascript
// Too many cache misses
// Origin server overwhelmed
// Solution: Rate limiting, cache warming
```

### 3. SSL/TLS Termination
```javascript
// HTTPS termination at edge
// Certificate management
// Solution: CDN SSL, custom certificates
```

### 4. Cache Poisoning
```javascript
// Malicious content cached
// Served to users
// Solution: Cache validation, purge
```

### 5. Stale Content
```javascript
// Old content served
// Origin updated but cache not invalidated
// Solution: Proper cache headers, invalidation
```

### 6. Geographic Routing Issues
```javascript
// User routed to wrong edge
- Higher latency
// Solution: Better DNS, anycast
```

**Why Edge Cases Matter:**
- Cache stampede overwhelms origin
- Origin overload causes downtime
- SSL termination critical for security
- Cache poisoning affects all users
- Stale content causes confusion
- Geographic routing affects performance

## Variations / Extensions

### 1. Multi-CDN Strategy

```javascript
// Use multiple CDN providers
- Failover between CDNs
- Better availability
```

### 2. Edge Computing

```javascript
// Run code at edge
- Dynamic content generation
- Request transformation
```

### 3. Image Optimization

```javascript
// Optimize images at edge
- Resize, compress, format conversion
- Better performance
```

### 4. Video Streaming

```javascript
// Adaptive bitrate streaming
- HLS, DASH
- Better video experience
```

### 5. API Caching

```javascript
// Cache API responses at edge
- Reduce origin load
- Faster API responses
```

## Optimization Techniques

### 1. Cache Warming

**Preload Cache:**
```javascript
// Warm cache before traffic
- Preload popular content
- Better initial performance
```

### 2. Brotli Compression

**Compress Content:**
```javascript
// Use Brotli compression
- Smaller payloads
- Faster transfer
```

### 3. HTTP/2

**Use HTTP/2:**
```javascript
// Multiplexing, header compression
- Better performance
- Lower latency
```

### 4. Preconnect

**Preconnect to Origin:**
```javascript
// Preconnect to origin server
- Faster cache miss recovery
- Better performance
```

### 5. Trade-offs

**CDN Providers Comparison:**

| Provider | Features | Pricing | Use Case |
|----------|----------|---------|----------|
| Cloudflare | Free tier, security | Free + paid | Small to medium |
| AWS CloudFront | AWS integration | Pay as you go | AWS users |
| Akamai | Enterprise features | High cost | Enterprise |
| Fastly | Edge computing | Pay as you go | Dynamic content |

**When to Use Each:**
- Cloudflare: Free tier, security features
- AWS CloudFront: AWS ecosystem integration
- Akamai: Enterprise, high traffic
- Fastly: Edge computing, dynamic content

## Complexity Analysis

### Time Complexity

**Cache Hit: O(1)**
- Edge server lookup
- Immediate serve
- Constant time

**Cache Miss: O(n)**
- n = origin response time
- Network latency
- Origin processing time

**Cache Invalidation: O(m)**
- m = number of edge servers
- Propagation time
- Distributed invalidation

### Space Complexity

**Cache Storage: O(k)**
- k = total cached content
- Distributed across edge servers
- Replication factor

**Explanation:**
CDN cache hit is O(1) - edge server serves cached content immediately. Cache miss is O(n) where n is the origin response time including network latency and processing. Cache invalidation is O(m) where m is the number of edge servers that need to be updated. Space complexity is O(k) where k is the total cached content distributed across edge servers with some replication for availability.

## Real-world Applications

### 1. Static Asset Delivery

**Web Assets:**
- CSS, JavaScript, images
- Fonts, icons
- Example: Any website with static assets

### 2. Video Streaming

**Media Delivery:**
- Netflix, YouTube
- Adaptive bitrate streaming
- Example: Video platforms

### 3. Software Distribution

**Downloads:**
- Software updates
- Game patches
- Example: Steam, game launchers

### 4. API Caching

**API Responses:**
- REST API caching
- GraphQL caching
- Example: Public APIs

### 5. E-commerce

**Product Images:**
- Product photos
- Thumbnails
- Example: Amazon, Shopify

### 6. Mobile Apps

**App Content:**
- App updates
- In-app content
- Example: Mobile app stores

### 7. News Websites

**Content Delivery:**
- Articles, images
- Breaking news
- Example: News sites

### 8. Social Media

**User Content:**
- Profile pictures
- Posts, media
- Example: Facebook, Twitter

## Common Mistakes

### 1. No Cache Headers

**Mistake:**
```javascript
// No cache headers set
// Content not cached
// Poor performance
```

**Correct:**
```javascript
// Set appropriate cache headers
// Cache static content
// Better performance
```

**Why It Matters:**
- No caching = poor performance
- Every request hits origin
- Higher latency and costs

### 2. Too Long TTL

**Mistake:**
```javascript
// Very long TTL for dynamic content
// Stale content served
// Incorrect information
```

**Correct:**
```javascript
// Set appropriate TTL per content type
// Short TTL for dynamic content
// Long TTL for static content
```

**Why It Matters:**
- Too long TTL = stale content
- Users see old information
- Updates not reflected

### 3. No Cache Invalidation

**Mistake:**
```javascript
// Content updated but cache not invalidated
// Old content served
// Confusion for users
```

**Correct:**
```javascript
// Invalidate cache on updates
// Use versioned URLs
// Proper cache management
```

**Why It Matters:**
- No invalidation = stale content
- Updates not visible
- Poor user experience

### 4. Ignoring Mobile

**Mistake:**
```javascript
// Not optimizing for mobile
// Large files
// Poor mobile performance
```

**Correct:**
```javascript
// Optimize for mobile
- Smaller images
- Responsive design
// Better mobile experience
```

**Why It Matters:**
- Mobile users significant
- Poor mobile UX = lost users
- Mobile optimization critical

### 5. No Monitoring

**Mistake:**
```javascript
// No CDN monitoring
// Don't know cache hit rate
// Can't optimize
```

**Correct:**
```javascript
// Monitor CDN performance
// Track cache hit rate
// Set up alerts
```

**Why It Matters:**
- Monitoring essential for optimization
- Cache hit rate indicates effectiveness
- Alerts catch issues early

### 6. Single CDN Dependency

**Mistake:**
```javascript
// Single CDN provider
- Single point of failure
// Outage affects all users
```

**Correct:**
```javascript
// Use multiple CDN providers
- Failover capability
// Better availability
```

**Why It Matters:**
- Single CDN = single point of failure
- Outage affects all users
- Multi-CDN improves availability

## Advanced Concepts

### 1. Edge Computing

**Concept:**
Run code at edge servers.

**Features:**
- Dynamic content generation
- Request transformation
- Security filtering

### 2. Image Optimization

**Concept:**
Optimize images at edge.

**Features:**
- Resize, compress
- Format conversion
- Responsive images

### 3. Adaptive Bitrate Streaming

**Concept:**
Adjust video quality based on bandwidth.

**Features:**
- HLS, DASH
- Better video experience
- Bandwidth optimization

### 4. Multi-CDN Strategy

**Concept:**
Use multiple CDN providers.

**Features:**
- Failover capability
- Better availability
- Cost optimization

## Practice Thinking Guide

### How to Design CDN Strategy

**Key Questions to Ask:**

1. **What content to cache?**
   - Static assets (images, CSS, JS)
   - Dynamic content (API responses)
   - Example: "Cache static assets, cache some API responses"

2. **What TTL to set?**
   - Static content: long TTL
   - Dynamic content: short TTL
   - Example: "1 year for images, 5 minutes for API"

3. **How to handle invalidation?**
   - TTL-based, purge, versioning
   - Choose based on content type
   - Example: "Versioning for assets, purge for API"

4. **Which CDN provider?**
   - Cloudflare, AWS CloudFront, Akamai
   - Based on features, pricing
   - Example: "Cloudflare for free tier, AWS for integration"

5. **How to monitor?**
   - Cache hit rate, latency, errors
   - Set up alerts
   - Example: "Monitor cache hit rate, alert below 80%"

**Pattern Recognition:**

**Pattern 1: Static Asset CDN**
```
Content: Images, CSS, JS
Strategy: Long TTL, versioning
Solution: Cache static assets with versioning
```

**Pattern 2: API CDN**
```
Content: API responses
Strategy: Short TTL, edge computing
Solution: Cache API responses with short TTL
```

**Pattern 3: Video CDN**
```
Content: Video files
Strategy: Adaptive bitrate streaming
Solution: Use video-specific CDN features
```

**Pattern 4: Global CDN**
```
Content: Global audience
Strategy: Geographic distribution
Solution: Multi-region edge servers
```

**Pattern 5: Secure CDN**
```
Content: Sensitive data
Strategy: Security features, WAF
Solution: CDN with security features
```

**Decision Flowchart:**

```
CDN Decision:
├─ Static or dynamic content?
│        ├─ Static → Long TTL, versioning
│        └─ Dynamic → Short TTL, edge computing
├─ Global or local audience?
│        ├─ Global → Geographic distribution
│        └─ Local → Single region OK
├─ High or low traffic?
│        ├─ High → Enterprise CDN
│        └─ Low → Free tier CDN
└─ Security requirements?
         ├─ High → CDN with WAF, DDoS protection
         └─ Low → Basic CDN OK
```

**Example Analysis:**

**Scenario:** "Design CDN for e-commerce site"

**Analysis:**
1. Content: Product images, CSS, JS, some API responses
2. Strategy: Long TTL for assets, short TTL for API
3. Invalidation: Versioning for assets, purge for API
4. Provider: Cloudflare or AWS CloudFront
5. Monitoring: Cache hit rate, latency, errors
6. Solution: Multi-tier caching strategy

**Scenario:** "Design CDN for video streaming"

**Analysis:**
1. Content: Video files, thumbnails
2. Strategy: Adaptive bitrate streaming
3. Invalidation: TTL-based
4. Provider: Specialized video CDN
5. Monitoring: Bandwidth, latency, errors
6. Solution: Video-specific CDN features

## Summary

CDN (Content Delivery Network) is a distributed network of servers that deliver web content to users based on their geographic location, origin server, and the content delivery server. CDNs cache static content like images, videos, CSS, JavaScript, and other assets on edge servers located around the world. When a user requests content, the CDN serves it from the nearest edge server, reducing latency and improving performance. CDNs also handle high traffic loads, reduce bandwidth costs, and provide security features like DDoS protection. Content is cached based on cache headers and can be invalidated through TTL expiration, explicit invalidation, or versioning. CDNs also provide edge computing capabilities, allowing code to run at the edge for dynamic content generation, request transformation, and security filtering.

**Key Takeaways:**
- Reduces latency through geographic proximity
- Caches static content at edge servers
- Handles high traffic loads
- Reduces bandwidth costs
- Provides security features
- Edge computing for dynamic content
- Cache invalidation strategies
- Monitor cache hit rate and performance

**Mastery Checklist:**
- ✅ Understand CDN architecture
- ✅ Configure cache headers
- ✅ Implement cache invalidation
- ✅ Use version-based caching
- ✅ Implement edge computing
- ✅ Optimize for mobile
- ✅ Monitor CDN performance
- ✅ Handle CDN failures gracefully

