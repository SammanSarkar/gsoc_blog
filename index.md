# Google Summer of Code 2024: AI-Powered Editorial Generation for omegaUp

## About Me

I am a passionate competitive programmer, currently an Expert on Codeforces and 5★ on CodeChef. My love for competitive programming and teaching naturally aligns with omegaUp's mission of coding education. This was my first Google Summer of Code project, though I've contributed to open source projects before.

Previously, I worked as a Software Engineer Intern at Microsoft, where I gained valuable experience with generative AI, LLMs, and AI agents. I recently joined Microsoft full-time, where I continue to apply the knowledge gained from this project in my daily work with AI systems.

## Project Motivation

omegaUp's extensive problem library serves as a powerful learning tool for competitive programmers worldwide. However, a significant gap exists: many problems lack comprehensive editorials. This absence frustrates learners who need guidance after attempting problems, ultimately weakening the platform's educational impact.

The current editorial system relies entirely on manual creation by problem authors. While this approach maintains high quality control, it results in inconsistent coverage across the problem library due to the substantial time investment required from authors. Many excellent problems remain without editorials simply because authors don't have the time to write detailed explanations.

Generative AI presents an opportunity to bridge this content gap by automating editorial creation while maintaining quality through technical validation and human review processes.

## Project Goals

The primary objective was to develop an AI-powered system that could automatically generate high-quality problem editorials in multiple languages (English, Spanish, and Portuguese). The system needed to:

1. **Integrate seamlessly** with omegaUp's existing infrastructure
2. **Generate comprehensive editorials** including problem analysis, solution approaches, and working code
3. **Support multiple languages** to serve omegaUp's diverse user base
4. **Maintain quality standards** through verification and validation processes
5. **Scale efficiently** to handle high user demand
6. **Preserve editorial quality** while reducing manual effort

## Technical Implementation

The system provides a simple API that can be called for any problem on omegaUp. Here's exactly what happens when a user requests an editorial:

### Worker Flow
1. **Job Polling**: Python worker continuously polls Redis queue for new editorial generation jobs
2. **Authentication Setup**: Worker initializes API client using user's auth token and validates credentials
3. **AC Solution Discovery**: System searches through problem submissions to find an existing Accepted (AC) solution for reference
4. **3-Prompt AI Generation**: AI generates editorial using problem statement and AC solution, then creates its own C++ solution
5. **Solution Verification**: Generated C++ code is automatically submitted to omegaUp judge system and verdict is captured (AC/WA/TLE/etc.)
6. **Multi-language Translation**: Based on verification results, editorial is translated to Spanish and Portuguese with appropriate disclaimers

### Workflow Diagram
<img width="2042" height="741" alt="diagram-export-30-08-2025-20_24_28" src="https://github.com/user-attachments/assets/e9000034-4bbf-4783-af9a-54030a7ad32c" />


## Development Journey

### Pull Requests and Milestones

| Component | Description | PR Links |
|-----------|-------------|----------|
| **Prototype Development** | Initial system prototype and proof of concept | [https://github.com/omegaup/omegaup/pull/8337](https://github.com/omegaup/omegaup/pull/8337) |
| **Database Design** | Job tracking schema with rate limiting support | [https://github.com/omegaup/omegaup/pull/8346](https://github.com/omegaup/omegaup/pull/8346) |
| **Data Access Layer** | CRUD operations and business logic methods | [https://github.com/omegaup/omegaup/pull/8347](https://github.com/omegaup/omegaup/pull/8347) |
| **API Controller** | REST endpoints for generation, status, and review | [https://github.com/omegaup/omegaup/pull/8350](https://github.com/omegaup/omegaup/pull/8350) |
| **Unit Testing** | Comprehensive test coverage for API endpoints | [https://github.com/omegaup/omegaup/pull/8352](https://github.com/omegaup/omegaup/pull/8352) |
| **Worker Foundation** | Core worker with Redis polling and job management | [https://github.com/omegaup/omegaup/pull/8355](https://github.com/omegaup/omegaup/pull/8355) |
| **Configuration Management** | Config manager and Redis client components | [https://github.com/omegaup/omegaup/pull/8358](https://github.com/omegaup/omegaup/pull/8358), [https://github.com/omegaup/omegaup/pull/8361](https://github.com/omegaup/omegaup/pull/8361) |
| **Solution Handling** | AC solution discovery and verification system | [https://github.com/omegaup/omegaup/pull/8364](https://github.com/omegaup/omegaup/pull/8364) |
| **Editorial Generator** | Core AI integration and content generation | [https://github.com/omegaup/omegaup/pull/8368](https://github.com/omegaup/omegaup/pull/8368) |
| **Website Integration** | Editorial publishing and content management | [https://github.com/omegaup/omegaup/pull/8369](https://github.com/omegaup/omegaup/pull/8369) |
| **Authentication System** | User session integration and security | [https://github.com/omegaup/omegaup/pull/8373](https://github.com/omegaup/omegaup/pull/8373) |
| **Production Deployment** | Multiple PRs for production readiness and fixes | [https://github.com/omegaup/omegaup/pull/8384](https://github.com/omegaup/omegaup/pull/8384), [https://github.com/omegaup/omegaup/pull/8391](https://github.com/omegaup/omegaup/pull/8391), [https://github.com/omegaup/omegaup/pull/8396](https://github.com/omegaup/omegaup/pull/8396), [https://github.com/omegaup/omegaup/pull/8399](https://github.com/omegaup/omegaup/pull/8399), [https://github.com/omegaup/omegaup/pull/8401](https://github.com/omegaup/omegaup/pull/8401), [https://github.com/omegaup/omegaup/pull/8402](https://github.com/omegaup/omegaup/pull/8402), [https://github.com/omegaup/omegaup/pull/8403](https://github.com/omegaup/omegaup/pull/8403), [https://github.com/omegaup/omegaup/pull/8405](https://github.com/omegaup/omegaup/pull/8405), [https://github.com/omegaup/omegaup/pull/8407](https://github.com/omegaup/omegaup/pull/8407) |
| **Infrastructure Setup** | Kubernetes deployment and production configuration | [https://github.com/omegaup/prod/pull/22](https://github.com/omegaup/prod/pull/22), [https://github.com/omegaup/prod/pull/24](https://github.com/omegaup/prod/pull/24), [https://github.com/omegaup/prod/pull/25](https://github.com/omegaup/prod/pull/25), [https://github.com/omegaup/prod/pull/26](https://github.com/omegaup/prod/pull/26), [https://github.com/omegaup/prod/pull/27](https://github.com/omegaup/prod/pull/27) |

## User Workflow

The system provides a streamlined user experience:

1. **Request Generation**: Users click "Generate AI Editorial" on any problem page
2. **Real-time Status**: The interface displays job progress with live updates
3. **Content Delivery**: Completed editorials appear automatically in the user's preferred language
4. **Quality Review**: Users can provide feedback on editorial quality for continuous improvement

The entire process typically completes within 2-3 minutes, making it practical for interactive use during problem-solving sessions.

## Impact and Future Work

This project helps improve editorial coverage on omegaUp significantly. Currently, many problems lack editorials due to the time required to write them manually. With this automated system, we could potentially cover 70-80% of problems that don't have editorials, making the platform more helpful for learners.

The backend system is fully functional and ready for production. The next step would be integrating it with the frontend interface to make it accessible to users. The system can also be improved with better AI models. It also provides a foundation for other automated content generation features on omegaUp.

## Acknowledgments

Thanks to my mentors [Hugo](https://github.com/heduenas) and [Juan](https://github.com/pabo99) for their guidance throughout this project. The omegaUp team provided great support and a solid platform to build on.

I look forward to continuing my contributions to omegaUp and further developing this AI editorial system.

---

*This project was completed as part of Google Summer of Code 2025 with omegaUp.*
