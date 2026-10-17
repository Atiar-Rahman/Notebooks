প্রথমে একটা কথা বলি—DRF (Django REST Framework) সম্পূর্ণ শিখতে এক মাসে সবকিছু শেষ করতেই হবে, এমন নয়। তুমি যেহেতু Python ও Django নিয়ে কাজ করছ, তাই নিয়মিত প্র্যাকটিস করলে ধাপে ধাপে Production-level DRF শিখতে পারবে।

তোমার লক্ষ্য হবে শুধু টপিকের নাম মুখস্থ করা নয়; নিজে API তৈরি করা, database design করা, security implement করা এবং production-এ deploy করতে পারা।

# DRF সম্পূর্ণ শেখার রোডম্যাপ (Beginner → Advanced → Production)

তোমার জন্য প্রস্তাবিত শেখার সময়

# ৪–৬ মাস

প্রতিদিন ২ ঘণ্টা করে Theory + Coding + Practice করলে এই সময়ের মধ্যে শক্ত ভিত্তি তৈরি করা সম্ভব। আগে থেকেই Django ভালো জানলে কম সময়ও লাগতে পারে।

## ১–২ মাস

Core DRF ও CRUD API

## ৩–৪ মাস

Advanced API ও Security

## ৫ম মাস

Testing ও Architecture

## ৬ষ্ঠ মাস

Production Project ও Deployment

এটা কোনো বাধ্যতামূলক সময়সীমা নয়। কিছু বিষয় দ্রুত শিখবে, কিছু বিষয়ে বেশি অনুশীলন প্রয়োজন হবে।

# Part 1: Prerequisites — DRF-এর আগে যা জানতে হবে

সময়: ১–৩ সপ্তাহ, তোমার বর্তমান দক্ষতার ওপর নির্ভর করে।

### Foundation Checklist

0/29

#### Python

Variables, data types, operators

Conditions, loops

Functions, arguments, *args, **kwargs

List, tuple, set, dictionary

List/dict comprehension

OOP: class, object, inheritance, polymorphism

Exception handling

Modules, packages, imports

Decorators, iterators, generators

Type hints, virtual environment, pip

#### Django

Project ও app structure

settings.py, urls.py, views.py

Models, fields, relationships

Migrations

Django ORM ও QuerySets

Function-based ও class-based views

Forms ও model validation

Middleware

Authentication ও permissions

Signals ও custom managers

#### Web ও Database

HTTP request ও response

GET, POST, PUT, PATCH, DELETE

HTTP status codes

JSON ও serialization ধারণা

REST API principles

Client-server architecture

SQL: SELECT, INSERT, UPDATE, DELETE

Primary key, foreign key, JOIN

Git ও GitHub basics

# Part 2: DRF Core — Beginner Level

সময়: ২–৪ সপ্তাহ

এগুলো DRF-এর সবচেয়ে গুরুত্বপূর্ণ ভিত্তি।

### Core DRF Checklist

0/25

DRF কী এবং কেন ব্যবহার করা হয়

Django views বনাম DRF API views

REST API architecture

APIView

Request ও Response objects

JSONRenderer ও Browsable API

Serializer কী এবং কেন প্রয়োজন

Serializer ও ModelSerializer

serializer.data বনাম validated_data বনাম errors

serializer.is_valid() ও raise_exception

create() ও update() methods

Field-level validation

Object-level validation

validate() method

Model validation ও database constraints

Function-based API views: @api_view

GenericAPIView

ListAPIView ও RetrieveAPIView

CreateAPIView, UpdateAPIView, DestroyAPIView

ListCreateAPIView ও RetrieveUpdateDestroyAPIView

ViewSet ও ModelViewSet

DefaultRouter ও SimpleRouter

URL routing ও nested URL patterns

HTTP status codes ও error responses

CRUD API implementation

এই Part শেষে Project: Product CRUD API — Product create, list, retrieve, update ও delete।

# Part 3: Authentication ও Authorization

সময়: ২–৩ সপ্তাহ

1. Django authentication system
    
2. `IsAuthenticated` ও `AllowAny`
    
3. `IsAdminUser`
    
4. `IsAuthenticatedOrReadOnly`
    
5. Custom permission classes
    
6. Object-level permissions
    
7. Custom user model
    
8. Email-based login
    
9. Session authentication
    
10. Basic authentication
    
11. Token authentication
    
12. JWT authentication
    
13. Simple JWT installation ও configuration
    
14. Access token ও refresh token
    
15. Token refresh ও rotation
    
16. Token blacklist
    
17. Logout ও token revocation
    
18. Registration API
    
19. Login API
    
20. Email verification
    
21. Resend verification email
    
22. Change password API
    
23. Forgot password ও reset password
    
24. Profile API
    
25. Email change ও confirmation
    
26. Role-based access control (RBAC)
    
27. User, Staff ও Admin permissions
    
28. Password validators
    
29. Authentication throttling
    
30. Secure authentication testing
    

এই Part শেষে Project: Complete Authentication API।

# Part 4: Querying, Filtering ও Pagination

সময়: ১–২ সপ্তাহ

1. `request.query_params`
    
2. Query parameter validation
    
3. Django ORM filtering
    
4. SearchFilter
    
5. OrderingFilter
    
6. `django-filter` integration
    
7. Custom filter classes
    
8. Filter by category, price, date ও status
    
9. Multiple filter combinations
    
10. Pagination overview
    
11. PageNumberPagination
    
12. LimitOffsetPagination
    
13. CursorPagination
    
14. Custom pagination classes
    
15. Pagination response customization
    
16. Search + Filter + Ordering + Pagination একসঙ্গে ব্যবহার
    
17. Query parameter documentation
    
18. Filtering ও pagination testing
    

এই Part শেষে Project: Product Catalog API।

# Part 5: Relationships ও Advanced Serializers

সময়: ২–৩ সপ্তাহ

1. ForeignKey relationships
    
2. OneToOneField relationships
    
3. ManyToManyField relationships
    
4. Nested serializers
    
5. Writable nested serializers
    
6. Nested read-only serializers
    
7. PrimaryKeyRelatedField
    
8. StringRelatedField
    
9. SlugRelatedField
    
10. HyperlinkedModelSerializer
    
11. SerializerMethodField
    
12. Custom serializer fields
    
13. Dynamic fields
    
14. Conditional fields
    
15. Context ব্যবহার
    
16. `source` attribute
    
17. `read_only` ও `write_only`
    
18. `required`, `allow_null` ও `allow_blank`
    
19. Bulk create ও bulk update
    
20. Nested create/update-এর transaction management
    
21. Circular serializer relationships
    
22. Large nested response optimization
    

এই Part শেষে Project: Category → Product → Product Image → Review API।

# Part 6: ViewSets, Routers ও API Architecture

সময়: ১–২ সপ্তাহ

1. APIView বনাম GenericAPIView বনাম ViewSet
    
2. ModelViewSet ও ReadOnlyModelViewSet
    
3. Custom ViewSet
    
4. `@action(detail=True)`
    
5. `@action(detail=False)`
    
6. `get_queryset()`
    
7. `get_serializer_class()`
    
8. `get_permissions()`
    
9. `perform_create()`
    
10. `perform_update()`
    
11. `perform_destroy()`
    
12. `get_object()`
    
13. Request lifecycle
    
14. Authentication → Permissions → Throttling
    
15. Content negotiation
    
16. Exception handling
    
17. Custom exception handler
    
18. Consistent API response structure
    
19. API versioning
    
20. Namespaces ও router configuration
    
21. Service layer ও business logic separation
    
22. Fat views এড়ানো
    
23. Reusable mixins ও base classes
    
24. API design conventions
    

এই Part শেষে Project: Role-based Multi-User API।

# Part 7: Permissions, Security ও Production Validation

সময়: ২–৩ সপ্তাহ

1. Authentication বনাম Authorization
    
2. Global ও view-level permissions
    
3. Object-level permission checks
    
4. Queryset-level data isolation
    
5. Multi-tenant data isolation
    
6. User ownership validation
    
7. Insecure Direct Object Reference (IDOR)
    
8. Mass assignment প্রতিরোধ
    
9. Sensitive fields exposure প্রতিরোধ
    
10. Input validation ও sanitization
    
11. SQL injection প্রতিরোধের ORM practices
    
12. XSS ও unsafe HTML handling
    
13. CSRF ও CORS-এর পার্থক্য
    
14. HTTPS ও secure cookies
    
15. JWT security considerations
    
16. Rate limiting ও throttling
    
17. Brute-force protection
    
18. Login enumeration প্রতিরোধ
    
19. Secure password reset
    
20. File upload validation
    
21. Environment variables ও secrets
    
22. Django security settings
    
23. `manage.py check --deploy`
    
24. Security audit checklist
    
25. Dependency vulnerability scanning
    

# Part 8: ORM Performance ও Database Engineering

সময়: ২–৪ সপ্তাহ

1. `select_related()`
    
2. `prefetch_related()`
    
3. N+1 query problem
    
4. `only()` ও `defer()`
    
5. `annotate()` ও `aggregate()`
    
6. `F()` ও `Q()` expressions
    
7. `Subquery` ও `OuterRef`
    
8. `Exists`
    
9. Conditional expressions: `Case` ও `When`
    
10. Window functions
    
11. `bulk_create()` ও `bulk_update()`
    
12. `transaction.atomic()`
    
13. `select_for_update()`
    
14. Database constraints
    
15. UniqueConstraint ও CheckConstraint
    
16. Database indexes
    
17. `QuerySet.explain()`
    
18. Query profiling
    
19. Race conditions
    
20. Concurrent requests
    
21. Database transaction isolation
    
22. PostgreSQL integration
    
23. Connection pooling ও PgBouncer basics
    
24. Idempotency
    
25. Optimistic ও pessimistic locking-এর ধারণা
    

এই Part শেষে Project: Inventory ও Order API, যেখানে concurrent stock update নিরাপদভাবে পরিচালিত হবে।

# Part 9: File Upload, Email, Cache ও Background Tasks

সময়: ২–৩ সপ্তাহ

1. `MultiPartParser`
    
2. `FormParser`
    
3. FileField ও ImageField
    
4. File upload serializer validation
    
5. File size ও content-type validation
    
6. Django `MEDIA_ROOT` ও `MEDIA_URL`
    
7. Cloud storage integration concepts
    
8. Email backend configuration
    
9. HTML ও plain-text email
    
10. Email verification workflow
    
11. Redis cache
    
12. Django cache framework
    
13. API response caching
    
14. Cache invalidation
    
15. Celery fundamentals
    
16. Background task scheduling
    
17. Retry ও exponential backoff
    
18. Task idempotency
    
19. `transaction.on_commit()`
    
20. Transactional outbox pattern
    
21. Celery monitoring
    
22. Redis broker ও failure handling
    

# Part 10: Testing ও Quality Assurance

সময়: ২–৩ সপ্তাহ

1. Django `TestCase`
    
2. DRF `APITestCase`
    
3. `APIClient`
    
4. `APIRequestFactory`
    
5. pytest ও pytest-django
    
6. Fixtures ও factories
    
7. Serializer unit tests
    
8. Model tests
    
9. API integration tests
    
10. Authentication tests
    
11. Permission tests
    
12. Object ownership tests
    
13. Validation error tests
    
14. Pagination ও filter tests
    
15. Database transaction tests
    
16. Mocking external APIs
    
17. Email testing
    
18. Celery task testing
    
19. Coverage measurement
    
20. Regression tests
    
21. Security tests
    
22. End-to-end testing
    
23. Continuous Integration (CI)
    

# Part 11: Documentation ও Developer Experience

সময়: ১ সপ্তাহ

1. OpenAPI specification
    
2. Swagger UI
    
3. ReDoc
    
4. `drf-spectacular`
    
5. Request ও response schemas
    
6. Serializer-based documentation
    
7. Authentication documentation
    
8. Error response schemas
    
9. API version documentation
    
10. Pagination documentation
    
11. Example requests ও responses
    
12. Postman collections
    
13. API contract testing
    
14. Backward compatibility
    

# Part 12: Performance ও Scalability

সময়: ২–৩ সপ্তাহ

1. API latency ও throughput
    
2. Response time profiling
    
3. Slow-query analysis
    
4. Response payload optimization
    
5. Database query count reduction
    
6. Caching strategies
    
7. Rate limiting
    
8. Gunicorn workers ও timeouts
    
9. Nginx reverse proxy
    
10. Redis caching
    
11. Locust load testing
    
12. Concurrent user simulation
    
13. p50, p95 ও p99 latency
    
14. Error rate ও throughput
    
15. Database connection budgeting
    
16. Memory ও CPU profiling
    
17. Pagination for large datasets
    
18. CDN ও object storage concepts
    
19. Horizontal scaling
    
20. Performance regression testing
    

# Part 13: Advanced API Patterns

সময়: ২–৪ সপ্তাহ

1. Custom authentication classes
    
2. Custom permission classes
    
3. Custom throttling classes
    
4. Custom pagination
    
5. Custom parsers ও renderers
    
6. Custom exception handlers
    
7. API versioning strategies
    
8. Polymorphic serializers
    
9. Generic relations
    
10. Bulk operations
    
11. Soft delete patterns
    
12. Audit logging
    
13. History tracking
    
14. Multi-tenant architecture
    
15. Idempotent payment APIs
    
16. Webhook signature verification
    
17. Webhook retries ও duplicate events
    
18. State machine for orders
    
19. Inventory reservation
    
20. Payment reconciliation
    
21. Filtering, sorting ও reporting APIs
    
22. Long-running jobs ও status endpoints
    
23. API deprecation strategy
    
24. Backward-compatible schema evolution
    

# Part 14: Deployment ও DevOps

সময়: ২–৪ সপ্তাহ

1. Development বনাম production settings
    
2. Environment-based configuration
    
3. PostgreSQL production configuration
    
4. Gunicorn
    
5. Dockerfile
    
6. Docker Compose
    
7. Non-root container user
    
8. Health checks
    
9. Static ও media files
    
10. Nginx reverse proxy
    
11. HTTPS ও TLS
    
12. Domain ও DNS
    
13. Firewall basics
    
14. Database migrations
    
15. Backup ও restore
    
16. GitHub Actions CI/CD
    
17. Docker image registry
    
18. Immutable image tags/digests
    
19. Staging ও production environments
    
20. Blue-green deployment
    
21. Expand/contract migrations
    
22. Rollback strategy
    
23. Structured logging
    
24. Error monitoring
    
25. Metrics ও alerting
    
26. Disaster recovery testing
    

# Part 15: বাস্তব Project — যা অবশ্যই তৈরি করবে

এই Project-গুলো ধারাবাহিকভাবে বানালে শেখা অনেক বেশি কার্যকর হবে।

![Creating views and serializers — Django Rest Framework | by Emre Cevik | Python | Django & Rest | Medium](https://images.openai.com/static-rsc-4/RO6B7S2WNROeAWYPrmMgY_N7mjFE5ZdxmsIZKCaG0ksMYuwZqTh9oLNidjSFCPyLEOyBumLqX6uT23Z4S2sIEpf6nSj7kMeG_2WlsaxzHMnzsWaX8qbDGk5PSCdi9nMVxRYdxF_eDYMkNTC9vNJqFVzBtVryjrsmKlFxw7Z1uUA?purpose=inline)

Project 1 — Product CRUD API

Beginner · ৩–৫ দিন

Models, serializers, ViewSets, CRUD, validation, filtering ও pagination।

![Join 88.2M+ Professionals | Sign Up Free | Freelancer](https://images.openai.com/static-rsc-4/yW1vX51qySzseg1NPZI8Wkl1GA4GeL7oE0DaQxtIZJAajmr4U9Oj38ze193CgEtYXz3iA1rufEvrK5Jm-0lK2qRFXx3mz-ItOReEDmHecx9QBKoU4aTd_aQYDwXjyjztjfKWXhiYiZ1yl104YrCkR0MvGKpFQogsFSz_mVw6QHQ?purpose=inline)

Project 2 — Complete Authentication System

Intermediate · ১–২ সপ্তাহ

Registration, email verification, JWT, password reset, profile, RBAC ও security tests।

![Sellzy - Multivendor eCommerce Web, Admin Dashboard Next.js Template by RiveupDigital](https://images.openai.com/static-rsc-4/ZW8R2Ia6GJ_-26QzKlTOvO5h05QuOpXnzSGiEsRJXU-KcayRws2aZgyK81CUUqW-jXBYtNx_g59h2X9NShwB200X-niH68O4-GKocXRx82wyPhjh3YVuazXv-Vtn1mvck-YVilC8ROFwCmyPTjgGHvkIfSaZ2xI_UxGGb1ACFzM?purpose=inline)

Project 3 — E-commerce Backend

Advanced · ৩–৫ সপ্তাহ

Products, variants, inventory, carts, orders, payments, webhooks, transactions ও concurrency।

![Four Zero Soft — Engineering Intelligent Systems for Scalable Businesses](https://images.openai.com/static-rsc-4/Vuh4fwCuL2HGReF5iXvJA9WRoPB4RgH5eQ7bMsNzBa0uX3OV40yoMg9Jt8WQmgFMrYGQ4YERBciivXn3sKG-EuTBN8kynhSVrOJjCejz4gzK1TDVQIr17pmH1gnKOYePbirHYh3lCSgl4Ze7-ZSbkT1hTKsUPiG8zQVOqoalTgg?purpose=inline)

Project 4 — Production API

Production · ২–৪ সপ্তাহ

Docker, PostgreSQL, Redis, Celery, Nginx, Gunicorn, CI/CD, monitoring, backup ও deployment।

# প্রতিদিন কীভাবে শিখবে?

তোমার জন্য ২ ঘণ্টার একটি নমনীয় রুটিন:

|সময়|কাজ|
|---|---|
|২০ মিনিট|আগের দিনের বিষয় রিভিশন|
|৩০ মিনিট|নতুন বিষয় বোঝা|
|৫০ মিনিট|নিজে কোড লেখা|
|২০ মিনিট|টেস্ট, ভুল ঠিক করা ও নোট|

সবচেয়ে গুরুত্বপূর্ণ নিয়ম: প্রতিদিন অনেকগুলো টপিক শেষ করার চেয়ে একটি টপিক বুঝে নিজে implement করা ভালো।

## এখন তোমার প্রথম লক্ষ্য

সব ১৫টি Part একসঙ্গে শেষ করার চিন্তা কোরো না। প্রথমে Part 1 ও Part 2 শেষ করো। তারপর authentication, database, security এবং production-এর দিকে এগোবে।

তুমি চাইলে নিচের বোতাম দিয়ে একদম গোড়া থেকে ধারাবাহিক ক্লাস শুরু করতে পারো।

## DRF Complete Course — Class 1

Django REST Framework কী, কেন ব্যবহার করা হয়, Django ও DRF-এর পার্থক্য, REST API কীভাবে কাজ করে এবং প্রথম API তৈরি—Theory + Code + Practice।

Class 1 শুরু করি

মনে রেখো, DRF শেখার জন্য প্রতিটি টপিক একবারে নিখুঁতভাবে শিখতে হবে না। প্রথমে কাজের API বানাতে শেখো, তারপর একই API-কে নিরাপদ, দ্রুত এবং production-ready করো। এভাবেই ধাপে ধাপে দক্ষতা তৈরি হবে।

----
