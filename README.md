# INTERNET-MUERTA
LENGUAJES MUERTOS
import React, { useState, useEffect } from 'react';

const DOSConverter = () => {
  const [twitterLink, setTwitterLink] = useState('');
  const [convertedLinks, setConvertedLinks] = useState<string[]>([]);
  const [followerLinks, setFollowerLinks] = useState<string[]>([]);
  const [error, setError] = useState<string | null>(null);
  const [loading, setLoading] = useState(false);

  const dosify = (link: string): string => {
    // Basic DOS-style conversion
    const dosLink = link.replace(/\//g, '\\').substring(0, 63); // DOS paths have length limit
    return dosLink;
  };

  const fetchAndConvertLinks = async () => {
    setLoading(true);
    setError(null);
    setConvertedLinks([]);
    setFollowerLinks([]);

    try {
      // Simulate fetching data from the Twitter link
      // In a real application, you would use a backend service to scrape the links
      await new Promise(resolve => setTimeout(resolve, 1000)); // Simulate network delay

      // Mock data - Replace with actual scraping logic
      const mockPageLinks = [
        'https://twitter.com/example1',
        'https://example.com/page2',
        'https://another-site.org/article',
      ];

      const mockFollowerLinks = [
        'https://twitter.com/follower1',
        'https://example.net/profile',
      ];

      const dosifiedPageLinks = mockPageLinks.map(link => dosify(link));
      const dosifiedFollowerLinks = mockFollowerLinks.map(link => dosify(link));

      setConvertedLinks(dosifiedPageLinks);
      setFollowerLinks(dosifiedFollowerLinks);
    } catch (err: any) {
      setError('Failed to fetch and convert links. Please check the URL.');
      console.error(err);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="flex flex-col items-center justify-start min-h-screen bg-gray-100 py-8 px-4">
      <h1 className="text-3xl font-bold text-gray-800 mb-6">Twitter Link to DOS Converter</h1>

      <div className="w-full max-w-md bg-white rounded-lg shadow-md p-6 mb-6">
        <label htmlFor="twitterLink" className="block text-gray-700 text-sm font-bold mb-2">
          Twitter Link:
        </label>
        <input
          type="text"
          id="twitterLink"
          className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mb-4"
          placeholder="Enter Twitter link"
          value={twitterLink}
          onChange={(e) => setTwitterLink(e.target.value)}
        />
        <button
          className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          onClick={fetchAndConvertLinks}
          disabled={loading}
        >
          {loading ? 'Converting...' : 'Convert to DOS'}
        </button>
      </div>

      {error && (
        <div className="bg-red-200 text-red-800 p-3 rounded-md mb-4 w-full max-w-md">
          {error}
        </div>
      )}

      {convertedLinks.length > 0 && (
        <div className="w-full max-w-md bg-white rounded-lg shadow-md p-6 mb-6">
          <h2 className="text-xl font-semibold text-gray-700 mb-3">Converted Page Links:</h2>
          <ul>
            {convertedLinks.map((link, index) => (
              <li key={index} className="text-gray-600">{link}</li>
            ))}
          </ul>
        </div>
      )}

      {followerLinks.length > 0 && (
        <div className="w-full max-w-md bg-white rounded-lg shadow-md p-6">
          <h2 className="text-xl font-semibold text-gray-700 mb-3">Converted Follower Links:</h2>
          <ul>
            {followerLinks.map((link, index) => (
              <li key={index} className="text-gray-600">{link}</li>
