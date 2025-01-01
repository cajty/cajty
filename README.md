import React, { useState, useEffect } from 'react';
import { GitHub, Linkedin, Mail, Phone, Book, Code, Database, Tools } from 'lucide-react';

const DeveloperProfile = () => {
  const [isVisible, setIsVisible] = useState({});
  
  useEffect(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          setIsVisible(prev => ({...prev, [entry.target.id]: true}));
        }
      });
    });

    document.querySelectorAll('section').forEach((section) => {
      observer.observe(section);
    });

    return () => observer.disconnect();
  }, []);

  return (
    <div className="max-w-4xl mx-auto p-8 bg-gradient-to-br from-gray-50 to-gray-100">
      <header className="text-center mb-12">
        <h1 className="text-4xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 mb-4">
          Ayoub Belyamane
        </h1>
        <p className="text-xl text-gray-700 mb-6">Transforming Ideas into Digital Reality</p>
        
        <div className="flex justify-center space-x-4">
          <SocialButton Icon={GitHub} href="https://github.com/cajty" />
          <SocialButton Icon={Linkedin} href="https://www.linkedin.com/in/belyamane-ayoub" />
          <SocialButton Icon={Mail} href="mailto:Belyamaneayoub1@gmail.com" />
          <SocialButton Icon={Phone} href="tel:+212623455637" />
        </div>
      </header>

      <section id="about" className={`mb-12 transform transition-all duration-700 ${isVisible.about ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'}`}>
        <div className="bg-white rounded-lg shadow-lg p-6">
          <h2 className="text-2xl font-semibold mb-4 flex items-center">
            <Code className="mr-2" /> Technical Expertise
          </h2>
          <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
            {['JavaScript', 'React', 'Angular', 'PHP', 'Laravel', 'Python'].map((skill) => (
              <SkillBadge key={skill} name={skill} />
            ))}
          </div>
        </div>
      </section>

      <section id="specializations" className={`mb-12 transform transition-all duration-700 ${isVisible.specializations ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'}`}>
        <div className="bg-white rounded-lg shadow-lg p-6">
          <h2 className="text-2xl font-semibold mb-4 flex items-center">
            <Database className="mr-2" /> Specializations
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            <SpecializationCard 
              title="Full Stack Development"
              description="Building scalable web applications with modern technologies"
            />
            <SpecializationCard 
              title="UI/UX Design"
              description="Creating intuitive and engaging user experiences"
            />
          </div>
        </div>
      </section>

      <section id="languages" className={`mb-12 transform transition-all duration-700 ${isVisible.languages ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'}`}>
        <div className="bg-white rounded-lg shadow-lg p-6">
          <h2 className="text-2xl font-semibold mb-4 flex items-center">
            <Book className="mr-2" /> Languages
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
            <LanguageCard language="Arabic" level="Native" flag="🇲🇦" />
            <LanguageCard language="English" level="B1" flag="🇬🇧" />
            <LanguageCard language="French" level="B2" flag="🇫🇷" />
          </div>
        </div>
      </section>
    </div>
  );
};

const SocialButton = ({ Icon, href }) => (
  <a
    href={href}
    className="p-2 rounded-full bg-gray-100 hover:bg-gray-200 transition-colors duration-300"
    target="_blank"
    rel="noopener noreferrer"
  >
    <Icon className="w-6 h-6 text-gray-700" />
  </a>
);

const SkillBadge = ({ name }) => (
  <div className="bg-blue-50 text-blue-700 px-4 py-2 rounded-full text-sm font-medium hover:bg-blue-100 transition-colors duration-300">
    {name}
  </div>
);

const SpecializationCard = ({ title, description }) => (
  <div className="bg-gray-50 p-4 rounded-lg hover:shadow-md transition-shadow duration-300">
    <h3 className="font-semibold text-lg mb-2">{title}</h3>
    <p className="text-gray-600">{description}</p>
  </div>
);

const LanguageCard = ({ language, level, flag }) => (
  <div className="bg-gray-50 p-4 rounded-lg text-center hover:shadow-md transition-shadow duration-300">
    <span className="text-2xl mb-2">{flag}</span>
    <h3 className="font-semibold">{language}</h3>
    <p className="text-gray-600">{level}</p>
  </div>
);

export default DeveloperProfile;
